## ¿Qué cambia?

<!-- Una o dos frases. Ej: "Agrega el display e-ink U4 al esquemático y su librería de símbolos." -->

## ¿Por qué?

<!-- El motivo de diseño. Ej: "El producto necesita mostrar el estado sin consumir energía en reposo." -->

## Tipo de cambio (versionado semántico de hardware)

- [ ] **MAJOR**: forma/tamaño de placa, voltajes de entrada/salida, nuevas interfaces (USB, conectores)
- [ ] **MINOR**: cambios de esquemático o layout
- [ ] **SUBREVISION**: solo BOM, valores o part numbers
- [ ] Solo documentación

## Checklist de revisión

- [ ] El esquemático abre sin errores en KiCad
- [ ] Corrí el ERC (*Inspect → Electrical Rules Checker*) y no hay errores nuevos
- [ ] Los componentes nuevos tienen referencia (U4, R3…) y valor
- [ ] No subí archivos generados (backups, `fp-info-cache`, `.kicad_prl`, gerbers)
- [ ] Los mensajes de commit siguen el formato `tipo(alcance): descripción`
- [ ] Actualicé el README si cambió algo que el usuario debe saber

## Capturas

<!-- Opcional: arrastra aquí una captura del esquemático antes/después. -->
