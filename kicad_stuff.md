# Export pcb to gerber files

First be sure to run `DRC` to check for errors and missing connections.

`File` -> `Plot`

`Output directory` - Set to directory relative to project.

Ensure following `Included Layers` are selected:
- [x] F.Cu
- [x] B.Cu
- [x] F.SilkS
- [x] B.SilkS
- [x] F.Mask
- [x] B.Mask
- [x] Edge.Cuts

Click `Plot` to generate plots.
 
Click `Generate Drill Files`.  Defaults are fine.

**Depending on board fabricator requirements** (e.g. JLPCB), check the `PTH and NPTH in a single file` box.

Click `Generate Drill File`

Check the generated files in KiCad's GerbView.

Zip files for upload to fabricator.
```shell
$ cd path_to_gerber_files
$ zip gerber_files.zip *
```
