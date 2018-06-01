<table align="center">
<tr><tr valign="top">
        <td width="354"><p align="center"><b><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Preview-Node">Preview</a></b></p>
<p align="center"><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Preview-Node"><img src="https://github.com/Unity-Technologies/ShaderGraph/wiki/Images/NodeLibrary/Nodes/Thumbnails/PreviewNodeThumb.png" alt="Preview Node" height="350" width="350"></a></p>
<p align="left">Provides a preview window and passes the input value through without modification.</p></td>
        <td width="354"><p align="center"><b><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Sub-graph-Node">Sub-graph</a></b></p>
<p align="center"><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Sub-graph-Node"><img src="https://github.com/Unity-Technologies/ShaderGraph/wiki/Images/NodeLibrary/Nodes/Thumbnails/SubgraphNodeThumb.png" alt="Sub-graph Node" height="350" width="350"></a></p>
<p align="left">Provides a reference to a Sub-graph asset.</p></td>
    </tr>
</table>

## Logic

<table align="center">
    <tr><tr valign="top">
        <td width="354"><p align="center"><b><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/All-Node">All</a></b></p>
<p align="center"><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/All-Node"><img src="https://github.com/Unity-Technologies/ShaderGraph/wiki/Images/NodeLibrary/Nodes/Thumbnails/AllNodeThumb.png" alt="All Node" height="350" width="350"></a></p>
<p align="left">Returns true if all components of the input In are non-zero.</p></td>
        <td width="354"><p align="center"><b><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/And-Node">And</a></b></p>
<p align="center"><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/And-Node"><img src="https://github.com/Unity-Technologies/ShaderGraph/wiki/Images/NodeLibrary/Nodes/Thumbnails/AndNodeThumb.png" alt="And Node" height="350" width="350"></a></p>
<p align="left">Returns true if both the inputs A and B are true.</p></td>
    </tr>
    <tr><tr valign="top">
         <td width="354"><p align="center"><b><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Any-Node">Any</a></b></p>
<p align="center"><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Any-Node"><img src="https://github.com/Unity-Technologies/ShaderGraph/wiki/Images/NodeLibrary/Nodes/Thumbnails/AnyNodeThumb.png" alt="Any Node" height="350" width="350"></a></p>
<p align="left">Returns true if any of the components of the input In are non-zero.</p></td>
        <td width="354"><p align="center"><b><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Branch-Node">Branch</a></b></p>
<p align="center"><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Branch-Node"><img src="https://github.com/Unity-Technologies/ShaderGraph/wiki/Images/NodeLibrary/Nodes/Thumbnails/BranchNodeThumb.png" alt="Branch Node" height="350" width="350"></a></p>
<p align="left">Provides a dynamic branch to the shader.</p></td>
    </tr>
    <tr><tr valign="top">
        <td width="354"><p align="center"><b><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Comparison-Node">Comparison</a></b></p>
<p align="center"><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Comparison-Node"><img src="https://github.com/Unity-Technologies/ShaderGraph/wiki/Images/NodeLibrary/Nodes/Thumbnails/ComparisonNodeThumb.png" alt="Comparison Node" height="350" width="350"></a></p>
<p align="left">Compares the two input values A and B based on the condition selected on the dropdown.</p></td>
        <td width="354"><p align="center"><b><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Is-Infinite-Node">Is Infinite</a></b></p>
<p align="center"><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Is-Infinite-Node"><img src="https://github.com/Unity-Technologies/ShaderGraph/wiki/Images/NodeLibrary/Nodes/Thumbnails/IsInfiniteNodeThumb.png" alt="Is Infinite Node" height="350" width="350"></a></p>
<p align="left">Returns true if any of the components of the input In is an infinite value.</p></td>
    </tr>
    <tr><tr valign="top">
        <td width="354"><p align="center"><b><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Is-NaN-Node">Is NaN</a></b></p>
<p align="center"><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Is-NaN-Node"><img src="https://github.com/Unity-Technologies/ShaderGraph/wiki/Images/NodeLibrary/Nodes/Thumbnails/IsNaNNodeThumb.png" alt="Is NaN Node" height="350" width="350"></a></p>
<p align="left">Returns true if any of the components of the input In is not a number (NaN).</p></td>
        <td width="354"><p align="center"><b><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Nand-Node">Nand</a></b></p>
<p align="center"><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Nand-Node"><img src="https://github.com/Unity-Technologies/ShaderGraph/wiki/Images/NodeLibrary/Nodes/Thumbnails/NandNodeThumb.png" alt="Nand Node" height="350" width="350"></a></p>
<p align="left">Returns true if both the inputs A and B are false.</p></td>
    </tr>
    <tr><tr valign="top">
        <td width="354"><p align="center"><b><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Not-Node">Not</a></b></p>
<p align="center"><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Not-Node"><img src="https://github.com/Unity-Technologies/ShaderGraph/wiki/Images/NodeLibrary/Nodes/Thumbnails/NotNodeThumb.png" alt="Not Node" height="350" width="350"></a></p>
<p align="left">Returns the opposite of input In. If In is true the output will be false, otherwise it will be true.</p></td>
        <td width="354"><p align="center"><b><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Or-Node">Or</a></b></p>
<p align="center"><a href="https://github.com/Unity-Technologies/ShaderGraph/wiki/Or-Node"><img src="https://github.com/Unity-Technologies/ShaderGraph/wiki/Images/NodeLibrary/Nodes/Thumbnails/OrNodeThumb.png" alt="Or Node" height="350" width="350"></a></p>
<p align="left">Returns true if either of the inputs A and B are true.</p></td>
    </tr>
</table>