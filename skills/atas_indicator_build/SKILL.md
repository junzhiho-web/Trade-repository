# ATAS Custom Indicator Build

## Set up the Visual Studio project

- Install Visual Studio Community and select the .NET desktop development workload. This is the only workload the build needs.

- Create a C# class library for .NET, not .NET Framework, and choose a name with no spaces. Select the .NET version that matches the ATAS 8 installation you are building against.

- Delete the default Class1.cs file. Add the indicator .cs file under the project node, not at the solution level, so the compiler includes it.

## Add references and compile

- Reference the ATAS platform DLLs from the ATAS installation folder. Use only the DLLs the indicator code needs and do not add OFT.Platform.exe.

- Add System.Drawing.Common from NuGet, not from the ATAS folder. The ATAS folder copy can be an older version and cause version errors.

- Build the solution and confirm the output says the build succeeded. Treat warnings as warnings and treat a missing DLL as failure.

## Hand off corrected code

- Deliver a corrected file for whole-file replacement in the user's project, never instructions to hand-edit individual lines. Hand edits reintroduce errors and cost more session time than a fresh file.

- Keep statement terminators outside trailing comments. A `;` placed after `//` sits inside the comment, leaves the statement unterminated, and the compiler reports CS1002. Scan the file for `;` characters following `//` before delivering it.

- Warn the user when a Chinese IME is active that the fullwidth semicolon `；` looks identical to `;` but is not valid C#. Have the user paste corrected lines verbatim instead of retyping them.

- Treat a stale Visual Studio error list as untrusted. Save the file, rebuild with Ctrl+Shift+B, and only then judge the result. Double-clicking an error jumps to the true offending line, which may differ from the line just edited.

## Install and verify in ATAS

- For ATAS X, use Add custom indicator and select the built DLL. For classic ATAS 8, copy the DLL to `%APPDATA%\ATAS\Indicators`, then restart ATAS fully.

- Do not use the Documents ATAS Indicators folder for ATAS 8. Confirm the real folder by checking for recent indicator files or a Backups folder.

- Load a chart with a working data connection and enough history for the indicator to initialize. Add the indicator and confirm its expected drawings appear.

- Check the data history and the selected indicator before changing code when nothing renders.

## Available connectors

- Use `muse.connector_search` to find other connectors and `muse.skill_search` to find related skills.

- If nothing here fits, look on the web for a maintained API or MCP server and set it up with [Custom Connectors and MCPs](/opt/muse/skills/custom-connector-setup/SKILL.md), or build a custom connector.

## Alternatives for better results

- Replace the System.Drawing.Common reference with the NuGet package version that matches the project framework when the build error names that assembly.

- Confirm the exact Indicators folder path and restart ATAS before rebuilding when the DLL does not appear in ATAS.

- Copy the exact error text and change only the named reference or setting when a build error is unclear.