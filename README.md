# PAFScaff: Pairwise mApping Format reference-based scaffold anchoring and super-scaffolding.

PAFScaff is designed for mapping genome assembly scaffolds to a closely-related chromosome-level reference genome
assembly. It uses (or runs) [Minimap2](https://github.com/lh3/minimap2) to perform an efficient (if rough) all-
against-all mapping, then parses the output to assign assembly scaffolds to reference chromosomes.

Mapping is based on minimap2-aligned assembly scaffold ("Query") coverage against the reference chromosomes.
Scaffolds are "placed" on the reference scaffold with most coverage. Any scaffolds failing to map onto any
chromosome are rated as "Unplaced". For each reference chromosome, PAFScaff then "anchors" placed assembly
scaffolds starting with the longest assembly scaffold. Each placed scaffold is then assessed in order of
decreasing scaffold length. Any scaffolds that do not overlap with already anchored scaffolds in terms of the
Reference chromosome positions they map onto are also considered "Anchored". if `newprefix=X` is set, scaffolds
are renamed with the Reference chromosome they match onto. The original scaffold name and mapping details are
included in the description. Unplaced scaffolds are not renamed.

Finally, Anchored scaffolds are super-scaffolded by inserting gaps of `NnNnNnNnNn` sequence between anchored
scaffolds. The lengths of these gaps are determined by the space between the reference positions, modified by
overhanging query scaffold regions (min. length 10). The alternating case of these gaps makes them easy to
identify later.

See [PAFScaff.md](./PAFScaff.md), <https://slimsuite.github.io/pafscaff/> for more information. General SLiMSuite run documentation can be
found at <https://github.com/slimsuite/SLiMSuite>.

**NOTE:** PAFScaff is under development and documentation might be a bit sparse. Please contact the author or
post an issue on GitHub if you have any questions.

PAFScaff is available as part of SLiMSuite, or via a standalone GitHub repo at
<https://github.com/slimsuite/pafscaff>.

---

## Running PAFScaff

PAFScaff is written in Python 2.x and can be run directly from the commandline:

    python $CODEPATH/pafscaff.py [OPTIONS]

If running as part of [SLiMSuite](http://slimsuite.blogspot.com/), `$CODEPATH` will be the SLiMSuite `tools/`
directory. If running from the standalone [PAFScaff git repo](https://github.com/slimsuite/pafscaff), `$CODEPATH`
will be the path the to `code/` directory. Please see details in the [PAFScaff git repo](https://github.com/slimsuite/pafscaff)
for running on example data.

To generate the PAF file, [minimap2](https://github.com/lh3/minimap2) must be installed and either added to the
environment `$PATH` or given to PAFScaff with the `minimap2=PROG` setting.


