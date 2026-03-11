```javascript
function ermittleTopStation(logs, suchMonat, minDauer) {
	const stationenSummen = new Map();
	
	for (const el of logs) {
		if (el.getMonat() == suchMonat &&
			el.getDauerMinuten() >= minDauer) 
			{ 
					stationenSummen.set(el.getStationenID(),(stationenSummen.get( el.getStationenID() + el.getGeladeneKWh());
			}
		}
	let StationIDMitMaximalemVerbrauch = -1;
    let maxSumme = -1;
    
    for (const [id, summe] of stationenSummen) {
        if (summe > maxSumme) {
            maxSumme = summe;
            StationIDMitMaximalemVerbrauch = id;
        }
    }
    
    return StationIDMitMaximalemVerbrauch;
}
```

