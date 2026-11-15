# Eccentric Pad Footing Design to ACI 318

A browser calculator for an isolated rectangular footing with the column off centre, such as a footing held back from a property line or one shifted to balance a column moment. It designs to ACI 318-25 or 318-19 in SI units. Enter the column and its position on the footing, the service and factored loads with their signs, the soil data, the footing size and the bars, then click Calculate. Every step shows the formula, the numbers used and the code clause, and each check is marked pass or fail.

## What it checks

- Materials, 75 mm bottom cover (Table 20.5.1.3.1), top cover where top bars are used, and depth above the bottom bars of at least 150 mm (13.3.1.2)
- Soil pressure under service loads with the column offset, moments and horizontal loads. When the resultant falls outside the kern, the app solves for the pressure on the part of the base still in contact, in one or both directions. It checks the maximum pressure against a net or gross allowable value and the share of the base in contact against a minimum you set
- Overturning about the edge each applied moment acts toward, and sliding, with a factor of safety of 1.5
- Factored contact pressure, with the factored weight of the footing and soil included, so any part of the footing that the soil does not hold up is designed for hogging
- Flexure at both column faces in both directions, minimum steel (8.6.1.1), the strain limit (8.3.3.1), the short-direction band (13.3.3.3) centred on the column as far as the footing allows, and top bars where hogging occurs
- One-way shear at d from both faces in both directions (Table 22.5.5.1 row (c), size effect neglected under 13.2.6.2 unless you switch it on)
- Punching shear at d/2 with interior, edge or corner sections and αs = 40, 30 or 20, and moment transfer about the centroid of the section (22.6, 8.4.4.2)
- Bearing on the column and the footing with A2 limited by the nearest edge (22.8.3.2), dowel area (16.3.4.1) and dowel development in compression (25.4.9.2)
- Bar spacing (8.7.2.2, 25.2.1) and development past each column face, reduced for excess steel (25.4.2.3, 25.4.10.1)

The results show the service and factored pressure plans with the lifted-off area, the zero-pressure line, the resultant and the critical sections. They also have a plan of the reinforcement, a section through the column with the contact pressure, a summary table and a bar schedule. The input panel shows where to put the column for uniform pressure, the soil utilisation, the smallest thickness that passes shear, the bars each direction needs and any top steel. You can export the full calculation as a PDF or an Excel workbook.

## How to use it

Open `index.html` in a web browser. Nothing needs installing, and everything runs on your computer, so no data leaves the page. The PDF and Excel libraries are in the `lib` folder, which must stay next to `index.html`.

Axes and signs: x runs along L and y along B, from the footing centre. A positive column offset moves the column toward +x or +y. A positive moment about y raises the pressure at the +x edge, and a positive moment about x raises it at the +y edge. Positive horizontal loads and shears act toward +x or +y. A moment that works against the offset is entered as negative.

To put it online, turn on GitHub Pages for this repository (Settings, then Pages, then deploy from the main branch).

## Method

The base is split into a 160 × 160 grid. The soil pressure is a plane, cut off at zero, whose resultant matches the total load and both moments; it is found by Newton iteration and matches the closed-form results for uniaxial partial contact. Moments and shears at each section come from integrating the design pressure (contact pressure less factored self weight) over the grid beyond that section. With the column at the centre, the results agree with the concentric pad footing calculator.

## Limits

- Rigid rectangular footing on soil with a linear pressure. No strap or tie beam, so all the eccentricity goes into the soil.
- One bottom mat of straight bars plus optional top bars, no shear reinforcement, normal-weight concrete, uncoated bars, compression in the column, nonseismic design.
- The full factored column moments are taken as transferred by eccentric shear in the punching check, which is conservative.
- Not covered: strap and combined footings, pile caps, uplift, settlement, hooked bar anchorage and seismic design.
- For ACI 318-25, the 2025 lower bound on one-way shear Vc is not used, which is conservative, and straight-bar development follows the 318-19 form.

This is a design aid. Results should be checked by a qualified engineer.

## Third-party libraries

- [jsPDF](https://github.com/parallax/jsPDF) and [jsPDF-AutoTable](https://github.com/simonbengtsson/jsPDF-AutoTable), MIT licence
- [SheetJS Community Edition](https://github.com/SheetJS/sheetjs), Apache 2.0 licence
- [DejaVu Sans](https://dejavu-fonts.github.io/) font, subset and embedded for PDF output, free licence

Developed by Aarakshya Kandel
