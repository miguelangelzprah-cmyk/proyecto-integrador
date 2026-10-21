# Arquitectura por capas

```mermaid
flowchart TB
  subgraph Usuarios["👥 Usuarios"]
    N(["🌐 Navegador"])
  end
  subgraph Seguridad["🛡️ Seguridad"]
    F{{"🔥 Firewall UFW"}}
  end
  subgraph Servicios["⚙️ Servicios"]
    NG[["🚀 Nginx"]]
    APP["📦 Aplicación"]
    BD[("🗄️ Base de datos")]
    NG --> APP --> BD
  end
  subgraph Operacion["🔧 Operación"]
    PG[/"📊 Prometheus + Grafana"/]
    BK[\"💾 Backup nocturno"\]
  end

  N == HTTPS ==> F
  F == "80 / 443" ==> NG
  PG -. métricas .-> NG
  BK -. respaldo .-> BD

  classDef user fill:#e3f2fd,stroke:#1565c0,stroke-width:2px,color:#0d47a1
  classDef sec fill:#ffebee,stroke:#c62828,stroke-width:2px,color:#b71c1c
  classDef srv fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#1b5e20
  classDef db fill:#fff3e0,stroke:#ef6c00,stroke-width:2px,color:#e65100
  classDef ops fill:#f3e5f5,stroke:#6a1b9a,stroke-width:2px,color:#4a148c
  class N user
  class F sec
  class NG,APP srv
  class BD db
  class PG,BK ops

  style Usuarios fill:#f5faff,stroke:#1565c0,stroke-dasharray:5 5
  style Seguridad fill:#fff5f5,stroke:#c62828,stroke-dasharray:5 5
  style Servicios fill:#f6fbf6,stroke:#2e7d32,stroke-dasharray:5 5
  style Operacion fill:#fbf5fc,stroke:#6a1b9a,stroke-dasharray:5 5
```

## Leyenda

| Forma | Significado |
|-------|-------------|
| Óvalo | Cliente o usuario |
| Hexágono | Seguridad (firewall) |
| Rectángulo con barras | Servicio expuesto (Nginx) |
| Cilindro | Almacenamiento de datos |
| Paralelogramo | Operación y mantenimiento |
| Flecha gruesa | Tráfico de usuarios |
| Flecha punteada | Métricas y respaldos |
