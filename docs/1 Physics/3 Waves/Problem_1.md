<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Wave Interference Pattern</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 900px;
            margin: 0 auto;
            padding: 30px;
            background-color: #f9f9f9;
            color: #333;
            line-height: 1.6;
        }

        h1, h2 {
            color: #005a9c;
        }

        img {
            max-width: 100%;
            height: auto;
            border-radius: 10px;
            border: 1px solid #ccc;
            margin-top: 20px;
        }

        code {
            background: #f4f4f4;
            padding: 2px 4px;
            border-radius: 4px;
        }

        pre {
            background: #f4f4f4;
            padding: 10px;
            overflow-x: auto;
            border-radius: 6px;
        }
    </style>
</head>
<body>

    <h1>🌊 Interference Pattern on a Water Surface</h1>

    <h2>🎯 Objective</h2>
    <p>Visualize and analyze the interference pattern created by circular water waves emitted from three point sources placed at the vertices of an equilateral triangle.</p>

    <h2>🧠 Background</h2>
    <p>Interference occurs when multiple waves overlap. If waves are in phase, they amplify each other (constructive interference); if out of phase, they cancel out (destructive interference). On a water surface, this creates visible ripple patterns.</p>

    <h2>🧾 Wave Equation</h2>
    <p>The displacement at any point on the water surface due to a single wave source is given by:</p>

    <pre>
ψ(x, y, t) = A · cos(k·r - ω·t + φ)
    </pre>

    <ul>
        <li><strong>A</strong>: amplitude</li>
        <li><strong>λ</strong>: wavelength</li>
        <li><strong>k = 2π/λ</strong>: wave number</li>
        <li><strong>ω = 2π·f</strong>: angular frequency</li>
        <li><strong>r</strong>: distance from wave source to point (x, y)</li>
        <li><strong>φ</strong>: initial phase (0 for all sources)</li>
    </ul>

    <h2>📈 Result</h2>
    <p>The image below shows the result of wave superposition from 3 coherent sources arranged in a triangle:</p>

    <img src="interference_plot.png" alt="Wave Interference Pattern">

    <p><strong>🔴 Red zones:</strong> Constructive interference (waves reinforce).<br>
       <strong>🔵 Blue zones:</strong> Destructive interference (waves cancel).<br>
       <strong>⚫ Black dots:</strong> Positions of wave sources.</p>

    <h2>📌 Conclusion</h2>
    <p>This visualization demonstrates how symmetry in source placement results in structured, predictable interference patterns. The triangle setup leads to 3-fold symmetry and a repeating interference grid.</p>

    <h2>🧪 Try This!</h2>
    <ul>
        <li>Change the polygon (e.g., square, pentagon) and observe how patterns change.</li>
        <li>Add time animation for dynamic wave visualization.</li>
        <li>Introduce phase shifts to explore wave coherence.</li>
    </ul>

</body>
</html>
