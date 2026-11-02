---
tipo: "indice"
area: "sistema"
fecha: 2026-11-02
estado: "activo"
tags: ["sistema", "dashboard"]
---

# 🎛️ CEREBRO — Dashboard

## 📋 Proyectos activos
```dataview
TABLE proyecto AS "Proyecto", siguiente_accion AS "Siguiente paso", prioridad AS "Prioridad"
FROM "03_Proyectos"
WHERE tipo = "proyecto" AND estado = "activo"
SORT prioridad ASC
```

## 🏋️ Volumen semanal (últimas 8 semanas)
```dataviewjs
const pages = dv.pages('"01_Ejercito/04_Preparacion_Fisica"').where(p => p.tipo === "entrenamiento" && p.fecha);
const semanas = {};
for (const p of pages) {
  const lunes = dv.date(p.fecha).startOf("week").toFormat("yyyy-LL-dd");
  semanas[lunes] ??= { kg: 0, km: 0, min: 0 };
  semanas[lunes].kg += Number(p.volumen_kg) || 0;
  semanas[lunes].km += Number(p.distancia_km) || 0;
  semanas[lunes].min += Number(p.duracion_min) || 0;
}
const claves = Object.keys(semanas).sort().slice(-8);
if (!claves.length) {
  dv.paragraph("Sin entrenamientos registrados.");
} else {
  const max = Math.max(...claves.map(k => semanas[k].kg), 1);
  for (const k of claves) {
    const s = semanas[k];
    const fila = dv.el("div", "", { attr: { style: "display:flex;align-items:center;gap:8px;margin:2px 0" } });
    fila.createEl("span", { text: k, attr: { style: "width:90px;font-family:monospace" } });
    fila.createEl("div", { attr: { style: `height:14px;width:${Math.round(s.kg / max * 300)}px;background:var(--interactive-accent);border-radius:3px` } });
    fila.createEl("span", { text: `${s.kg} kg · ${s.km.toFixed(1)} km · ${s.min} min` });
  }
}
```

## 🏃 Entrenamientos (últimos 14 días)
```dataview
TABLE modalidad AS "Modalidad", duracion_min AS "Min", distancia_km AS "Km", carga_ruck_kg AS "Carga kg", rpe AS "RPE"
FROM "01_Ejercito/04_Preparacion_Fisica"
WHERE tipo = "entrenamiento" AND fecha >= date(today) - dur(14 days)
SORT fecha DESC
```

## 🎓 Asignaturas
```dataview
TABLE asignatura AS "Asignatura", trimestre AS "Trimestre", estado AS "Estado"
FROM "02_Estudios"
WHERE tipo = "asignatura"
SORT trimestre ASC
```

## ⏱️ Horas de estudio por asignatura
```dataview
TABLE sum(rows.horas_estudio) AS "Horas", length(rows) AS "Sesiones"
FROM "02_Estudios"
WHERE tipo = "sesion_estudio"
GROUP BY asignatura
```

## 📝 Últimas sesiones de estudio
```dataview
TABLE asignatura AS "Asignatura", horas_estudio AS "Horas"
FROM "02_Estudios"
WHERE tipo = "sesion_estudio"
SORT fecha DESC
LIMIT 5
```
