# Výzkum LiDAR & RoomPlan API

Komplexní průvodce technologií Apple RoomPlan API a LiDAR skenování pro iOS aplikace.

## 📋 Obsah dokumentace

1. **[Úvod do RoomPlan](./01-uvod-roomplan.md)** - Co je RoomPlan API a jak funguje
2. **[LiDAR Technologie](./02-lidar-technologie.md)** - Principy LiDAR skenování
3. **[Architektura aplikace](./03-architektura.md)** - Struktura a návrh aplikace
4. **[API Reference](./04-api-reference.md)** - Detailní popis RoomPlan API
5. **[Příklady kódu](./05-priklady-kodu.md)** - Praktické implementace
6. **[Best Practices](./06-best-practices.md)** - Osvědčené postupy

## 🎯 O projektu

Tento výzkumný projekt dokumentuje využití Apple RoomPlan API a LiDAR technologie pro vytváření 3D půdorysů místností. Projekt vychází z analýzy open-source implementace [markckim/RoomPlan](https://github.com/markckim/RoomPlan).

## 🔑 Klíčové funkce RoomPlan

- **3D Mapování místností** pomocí LiDAR skeneru
- **Automatická detekce objektů** (nábytek, spotřebiče, atd.)
- **Real-time vizualizace** 3D scény
- **Export dat** do různých formátů (USDZ, JSON)
- **Kategorizace objektů** s možností úprav
- **Inteligentní umístění objektů** s detekcí rizik

## 📱 Požadavky

- **iOS 16+**
- **Zařízení s LiDAR skenerem:**
  - iPhone 12 Pro a novější
  - iPad Pro (4. generace a novější)
- **Xcode 14+**
- **Swift 5.7+**

## 🚀 Základní použití

```swift
import RoomPlan

// Vytvoření capture session
let captureSession = RoomCaptureSession()

// Konfigurace
var config = RoomCaptureSession.Configuration()
config.isCoachingEnabled = true

// Spuštění skenování
captureSession.run(configuration: config)

// Implementace delegate
extension ViewController: RoomCaptureSessionDelegate {
    func captureSession(_ session: RoomCaptureSession, didUpdate room: CapturedRoom) {
        // Zpracování aktualizací místnosti
    }
}
```

## 📊 Podporované kategorie objektů

RoomPlan automaticky rozpoznává:
- Nábytek (stoly, židle, pohovky, postele)
- Spotřebiče (ledničky, sporáky, pračky)
- Sanitární vybavení (umyvadla, toalety, vany)
- Další prvky (schody, krby, obrazovky)

## 🔬 Technické poznatky

### LiDAR Technologie
- Měří vzdálenost pomocí laserových paprsků
- Pracuje v infračerveném spektru
- Dosah až 5 metrů
- Přesnost na úrovni milimetrů

### ARKit Integrace
- RoomPlan využívá ARKit framework
- Kombinuje LiDAR s kamerou a pohybovými senzory
- Real-time tracking a mapování prostoru

## 📚 Zdroje

- [Apple RoomPlan Documentation](https://developer.apple.com/documentation/roomplan)
- [WWDC 2022: Create parametric 3D room scans](https://developer.apple.com/videos/play/wwdc2022/10127/)
- [Reference implementace: markckim/RoomPlan](https://github.com/markckim/RoomPlan)

## 🤝 Přispění

Tento projekt je určen pro výzkumné a vzdělávací účely. Návrhy na zlepšení jsou vítány!

## 📄 Licence

Tento výzkumný materiál je určen pro vzdělávací účely.

## 👤 Autor

**MEVERIK-SOLUTION**  
Vytvořeno: 2026-02-14

---

**Poznámka:** Dokumentace je průběžně aktualizována na základě nových poznatků a vývoje technologie.