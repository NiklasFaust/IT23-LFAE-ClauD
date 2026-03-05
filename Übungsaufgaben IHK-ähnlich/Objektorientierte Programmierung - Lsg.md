```c#
createFahrzeug(typ: string) 
{
 switch(typ): 
 {
  case "verbrenner": { return new Verbrenner(); } 
  case "elektro": { return new EAuto(); } 
  case "transporter": { return new Transporter(); } 
  case Default: { return null; } 
  } 
  }
```

```c#
FUNCTION createFahrzeug(typ, tagespreis)  
IF typ == "VERBRENNER" THEN RETURN new Verbrenner(tagespreis)  
ELSE IF typ == "E-AUTO" THEN RETURN new EAUTO(tagespreis)  
ELSE IF typ == "TRANSPORTER" THEN RETURN new Transporter(tagespreis)  
ELSE RETURN null  
END FUNCTION
```

#  d)
``` c#
Override berechneMiete() 
{ 
  float finalpreis =(this.tagespreis*this.tagesanzahl) / this.förderungsrabatt; 
  return finalpreis; 
}
```
