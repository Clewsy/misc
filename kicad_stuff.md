# Export pcb to gerber files

First be sure to run `DRC` to check for errors and missing connections.

`File` -> `Plot`

`Output directory` - Set to directory relative to project.

Ensure following `Included Layers` are selected:
1. F.Cu
2. B.Cu
3. F.SilkS
4. B.SilkS
5. F.Mask
6. B.Mask
7. Edge.Cuts

Click `Plot` to generate plots.
 
Click `Generate Drill Files`.  Defaults are fine.

**Depending on board fabricator requirements** (e.g. JLPCB), check the `PTH and NPTH in a single file` box.

Click `Generate Drill File`

Check the generated files in KiCad's GerbView.

Zip files for upload to fabricator.
```shell
$ cd [path_to_gerber_files]
$ zip gerber_files.zip *
```