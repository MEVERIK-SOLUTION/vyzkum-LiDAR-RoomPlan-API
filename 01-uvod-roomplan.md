# 1. Úvod do RoomPlan API

## Co je RoomPlan?

RoomPlan je Swift API od Apple, které bylo představeno na WWDC 2022 jako součást iOS 16. Umožňuje vývojářům vytvářet 3D půdorysy místností pomocí kombinace kamery a LiDAR skeneru na iPhone a iPad.

## Hlavní komponenty

### 1. RoomCaptureSession

Hlavní třída pro správu skenování místnosti.

```swift
let captureSession = RoomCaptureSession()
```

**Klíčové vlastnosti:**
- Spravuje ARSession
- Koordinuje LiDAR, kameru a senzory
- Poskytuje real-time updates
- Automaticky detekuje objekty a povrchy

### 2. RoomCaptureSessionDelegate

Protokol pro příjem událostí ze skenování.

```swift
protocol RoomCaptureSessionDelegate {
    // Nové objekty byly detekovány
    func captureSession(_ session: RoomCaptureSession, didAdd room: CapturedRoom)
    
    // Existující objekty byly aktualizovány
    func captureSession(_ session: RoomCaptureSession, didUpdate room: CapturedRoom)
    
    // Objekty změnily rozměry nebo pozici
    func captureSession(_ session: RoomCaptureSession, didChange room: CapturedRoom)
    
    // Objekty byly odstraněny
    func captureSession(_ session: RoomCaptureSession, didRemove room: CapturedRoom)
    
    // Pokyny pro uživatele
    func captureSession(_ session: RoomCaptureSession, didProvide instruction: RoomCaptureSession.Instruction)
    
    // Session byla zahájena
    func captureSession(_ session: RoomCaptureSession, didStartWith configuration: RoomCaptureSession.Configuration)
    
    // Session skončila
    func captureSession(_ session: RoomCaptureSession, didEndWith data: CapturedRoomData, error: Error?)
}
```

### 3. CapturedRoom

Reprezentuje naskenovanou místnost s objekty.

```swift
struct CapturedRoom {
    var walls: [CapturedRoom.Surface]
    var doors: [CapturedRoom.Surface]
    var windows: [CapturedRoom.Surface]
    var objects: [CapturedRoom.Object]
}
```

### 4. Configuration

Nastavení pro skenování.

```swift
var config = RoomCaptureSession.Configuration()
config.isCoachingEnabled = true  // Zobrazí pokyny pro uživatele
```

## Životní cyklus skenování

```
┌─────────────────┐
│  Inicializace   │
│  RoomCapture    │
│    Session      │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Konfigurace    │
│   & Start       │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Skenování     │◄─────┐
│  (didAdd,       │      │
│   didUpdate,    │      │
│   didChange)    │──────┘
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Ukončení      │
│  (didEndWith)   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Export dat     │
│  (USDZ, JSON)   │
└─────────────────┘
```

## Podporované kategorie objektů

RoomPlan automaticky rozpoznává tyto kategorie:

### Nábytek
- `storage` - Úložné prostory
- `bed` - Postele
- `table` - Stoly
- `sofa` - Pohovky
- `chair` - Židle

### Spotřebiče
- `refrigerator` - Ledničky
- `stove` - Sporáky
- `oven` - Trouby
- `dishwasher` - Myčky nádobí
- `washerDryer` - Pračky

### Sanitární vybavení
- `sink` - Umyvadla
- `toilet` - Toalety
- `bathtub` - Vany

### Další prvky
- `fireplace` - Krby
- `television` - Televizory/Obrazovky
- `stairs` - Schody

## Příklad implementace

```swift
import RoomPlan
import ARKit

class RoomScanViewController: UIViewController {
    
    lazy var captureSession: RoomCaptureSession = {
        let session = RoomCaptureSession()
        return session
    }()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        setupCaptureSession()
        startScanning()
    }
    
    func setupCaptureSession() {
        captureSession.delegate = self
    }
    
    func startScanning() {
        var config = RoomCaptureSession.Configuration()
        config.isCoachingEnabled = true
        
        captureSession.run(configuration: config)
    }
}

extension RoomScanViewController: RoomCaptureSessionDelegate {
    
    func captureSession(_ session: RoomCaptureSession, didAdd room: CapturedRoom) {
        print("Nové objekty: \(room.objects.count)")
        
        for object in room.objects {
            print("Objekt: \(object.category)")
            print("Rozměry: \(object.dimensions)")
            print("Pozice: \(object.transform)")
        }
    }
    
    func captureSession(_ session: RoomCaptureSession, didUpdate room: CapturedRoom) {
        print("Aktualizace místnosti")
    }
    
    func captureSession(_ session: RoomCaptureSession, didProvide instruction: RoomCaptureSession.Instruction) {
        switch instruction {
        case .moveCloseToWall:
            print("Přibližte se ke zdi")
        case .moveAwayFromWall:
            print("Oddalte se od zdi")
        case .slowDown:
            print("Zpomalte")
        case .turnOnLight:
            print("Zapněte světlo")
        case .normal:
            print("Pokračujte ve skenování")
        case .lowTexture:
            print("Málo textur - přidejte více detailů")
        @unknown default:
            break
        }
    }
    
    func captureSession(_ session: RoomCaptureSession, didEndWith data: CapturedRoomData, error: Error?) {
        if let error = error {
            print("Chyba: \(error)")
            return
        }
        
        // Export dat
        exportRoomData(data)
    }
    
    func exportRoomData(_ data: CapturedRoomData) {
        // Export do USDZ
        let url = FileManager.default.temporaryDirectory.appendingPathComponent("room.usdz")
        
        do {
            try data.export(to: url)
            print("Místnost exportována do: \(url)")
        } catch {
            print("Chyba exportu: \(error)")
        }
    }
}
```

## Výhody RoomPlan API

✅ **Automatická detekce** - Rozpoznává objekty bez manuálního označování  
✅ **Real-time feedback** - Okamžité vizualizace naskenovaných objektů  
✅ **Vysoká přesnost** - Díky kombinaci LiDAR a kamery  
✅ **Jednoduché API** - Snadná integrace do aplikací  
✅ **Export možnosti** - USDZ, JSON a další formáty  
✅ **Coaching mode** - Vestavěné pokyny pro uživatele  

## Omezení

⚠️ **Hardwarové požadavky** - Pouze zařízení s LiDAR skenerem  
⚠️ **iOS 16+** - Novější verze operačního systému  
⚠️ **Osvětlení** - Vyžaduje dostatečné osvětlení místnosti  
⚠️ **Velikost místnosti** - Optimální pro standardní místnosti (do 5m dosah)  
⚠️ **Kategorie objektů** - Omezený počet předefinovaných kategorií  

## Další kroky

- [2. LiDAR Technologie →](./02-lidar-technologie.md)
- [3. Architektura aplikace →](./03-architektura.md)

---

[← Zpět na hlavní stránku](./README.md)