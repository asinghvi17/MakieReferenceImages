## Ambient Occlusion

```@raw html
<pre class='hljl'>
<span class='hljl-t'>

</span><span class='hljl-k'>using</span><span class='hljl-t'> </span><span class='hljl-n'>AbstractPlotting</span><span class='hljl-t'>

</span><span class='hljl-n'>s1</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>radius</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>textslider</span><span class='hljl-p'>(</span><span class='hljl-nfB'>0.0f0</span><span class='hljl-oB'>:</span><span class='hljl-nfB'>0.1f0</span><span class='hljl-oB'>:</span><span class='hljl-nfB'>2f0</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-s'>&quot;Radius&quot;</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>start</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.2f0</span><span class='hljl-p'>)</span><span class='hljl-t'>
</span><span class='hljl-n'>s2</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>bias</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>textslider</span><span class='hljl-p'>(</span><span class='hljl-nfB'>0f0</span><span class='hljl-oB'>:</span><span class='hljl-nfB'>0.005f0</span><span class='hljl-oB'>:</span><span class='hljl-nfB'>0.1f0</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-s'>&quot;Bias&quot;</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>start</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.015f0</span><span class='hljl-p'>)</span><span class='hljl-t'>
</span><span class='hljl-n'>s3</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>blur</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>textslider</span><span class='hljl-p'>(</span><span class='hljl-nf'>Int32</span><span class='hljl-p'>(</span><span class='hljl-ni'>0</span><span class='hljl-p'>)</span><span class='hljl-oB'>:</span><span class='hljl-nf'>Int32</span><span class='hljl-p'>(</span><span class='hljl-ni'>1</span><span class='hljl-p'>)</span><span class='hljl-oB'>:</span><span class='hljl-nf'>Int32</span><span class='hljl-p'>(</span><span class='hljl-ni'>5</span><span class='hljl-p'>),</span><span class='hljl-t'> </span><span class='hljl-s'>&quot;Blur&quot;</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>start</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>Int32</span><span class='hljl-p'>(</span><span class='hljl-ni'>2</span><span class='hljl-p'>))</span><span class='hljl-t'>
</span><span class='hljl-n'>ssao_attrib</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>Attributes</span><span class='hljl-p'>(</span><span class='hljl-n'>radius</span><span class='hljl-oB'>=</span><span class='hljl-n'>radius</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>bias</span><span class='hljl-oB'>=</span><span class='hljl-n'>bias</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>blur</span><span class='hljl-oB'>=</span><span class='hljl-n'>blur</span><span class='hljl-p'>)</span><span class='hljl-t'>

</span><span class='hljl-n'>floor_pos</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-p'>[</span><span class='hljl-t'>
    </span><span class='hljl-nf'>Point3f0</span><span class='hljl-p'>(</span><span class='hljl-n'>x</span><span class='hljl-t'> </span><span class='hljl-oB'>+</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.05</span><span class='hljl-nf'>rand</span><span class='hljl-p'>(),</span><span class='hljl-t'> </span><span class='hljl-n'>y</span><span class='hljl-t'> </span><span class='hljl-oB'>+</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.05</span><span class='hljl-nf'>rand</span><span class='hljl-p'>(),</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.08</span><span class='hljl-nf'>rand</span><span class='hljl-p'>())</span><span class='hljl-t'>
    </span><span class='hljl-k'>for</span><span class='hljl-t'> </span><span class='hljl-n'>x</span><span class='hljl-t'> </span><span class='hljl-kp'>in</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.05</span><span class='hljl-oB'>:</span><span class='hljl-nfB'>0.1</span><span class='hljl-oB'>:</span><span class='hljl-nfB'>1.0</span><span class='hljl-t'> </span><span class='hljl-k'>for</span><span class='hljl-t'> </span><span class='hljl-n'>y</span><span class='hljl-t'> </span><span class='hljl-kp'>in</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.05</span><span class='hljl-oB'>:</span><span class='hljl-nfB'>0.1</span><span class='hljl-oB'>:</span><span class='hljl-nfB'>1.0</span><span class='hljl-t'>
</span><span class='hljl-p'>]</span><span class='hljl-t'>
</span><span class='hljl-n'>tile</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>Rect3D</span><span class='hljl-p'>(</span><span class='hljl-nf'>Point3f0</span><span class='hljl-p'>(</span><span class='hljl-oB'>-</span><span class='hljl-nfB'>0.8</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-oB'>-</span><span class='hljl-nfB'>0.8</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-oB'>-</span><span class='hljl-nfB'>0.3</span><span class='hljl-p'>),</span><span class='hljl-t'> </span><span class='hljl-nf'>Vec3f0</span><span class='hljl-p'>(</span><span class='hljl-nfB'>1.6</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>1.6</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.6</span><span class='hljl-p'>))</span><span class='hljl-t'>

</span><span class='hljl-n'>sphere_pos</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.8</span><span class='hljl-nf'>rand</span><span class='hljl-p'>(</span><span class='hljl-n'>Point3f0</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-ni'>50</span><span class='hljl-p'>)</span><span class='hljl-t'> </span><span class='hljl-oB'>.+</span><span class='hljl-t'> </span><span class='hljl-p'>[</span><span class='hljl-nf'>Point3f0</span><span class='hljl-p'>(</span><span class='hljl-nfB'>0.1</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.1</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.2</span><span class='hljl-p'>)]</span><span class='hljl-t'>
</span><span class='hljl-n'>sphere_colors</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>rand</span><span class='hljl-p'>(</span><span class='hljl-n'>RGBf0</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nf'>length</span><span class='hljl-p'>(</span><span class='hljl-n'>sphere_pos</span><span class='hljl-p'>))</span><span class='hljl-t'>
</span><span class='hljl-n'>sphere</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>Sphere</span><span class='hljl-p'>(</span><span class='hljl-nf'>Point3f0</span><span class='hljl-p'>(</span><span class='hljl-ni'>0</span><span class='hljl-p'>),</span><span class='hljl-t'> </span><span class='hljl-nfB'>1f0</span><span class='hljl-p'>)</span><span class='hljl-t'>

</span><span class='hljl-n'>scene1</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>Scene</span><span class='hljl-p'>(</span><span class='hljl-n'>SSAO</span><span class='hljl-oB'>=</span><span class='hljl-n'>ssao_attrib</span><span class='hljl-p'>)</span><span class='hljl-t'>
</span><span class='hljl-nf'>meshscatter!</span><span class='hljl-p'>(</span><span class='hljl-n'>scene1</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>floor_pos</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>marker</span><span class='hljl-oB'>=</span><span class='hljl-n'>tile</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>color</span><span class='hljl-oB'>=:</span><span class='hljl-n'>lightgray</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>ssao</span><span class='hljl-oB'>=</span><span class='hljl-kc'>true</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>shading</span><span class='hljl-oB'>=</span><span class='hljl-kc'>false</span><span class='hljl-p'>)</span><span class='hljl-t'>
</span><span class='hljl-nf'>meshscatter!</span><span class='hljl-p'>(</span><span class='hljl-n'>scene1</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>sphere_pos</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>marker</span><span class='hljl-oB'>=</span><span class='hljl-n'>sphere</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>color</span><span class='hljl-oB'>=</span><span class='hljl-n'>sphere_colors</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>ssao</span><span class='hljl-oB'>=</span><span class='hljl-kc'>true</span><span class='hljl-p'>)</span><span class='hljl-t'>

</span><span class='hljl-n'>scene2</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>Scene</span><span class='hljl-p'>()</span><span class='hljl-t'>
</span><span class='hljl-nf'>meshscatter!</span><span class='hljl-p'>(</span><span class='hljl-n'>scene2</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>floor_pos</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>marker</span><span class='hljl-oB'>=</span><span class='hljl-n'>tile</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>color</span><span class='hljl-oB'>=:</span><span class='hljl-n'>lightgray</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>ssao</span><span class='hljl-oB'>=</span><span class='hljl-kc'>false</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>shading</span><span class='hljl-oB'>=</span><span class='hljl-kc'>false</span><span class='hljl-p'>)</span><span class='hljl-t'>
</span><span class='hljl-nf'>meshscatter!</span><span class='hljl-p'>(</span><span class='hljl-n'>scene2</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>sphere_pos</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>marker</span><span class='hljl-oB'>=</span><span class='hljl-n'>sphere</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>color</span><span class='hljl-oB'>=</span><span class='hljl-n'>sphere_colors</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>ssao</span><span class='hljl-oB'>=</span><span class='hljl-kc'>false</span><span class='hljl-p'>)</span><span class='hljl-t'>

</span><span class='hljl-n'>scene</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>Scene</span><span class='hljl-p'>(</span><span class='hljl-n'>resolution</span><span class='hljl-oB'>=</span><span class='hljl-p'>(</span><span class='hljl-ni'>900</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-ni'>500</span><span class='hljl-p'>))</span><span class='hljl-t'>
</span><span class='hljl-nf'>hbox</span><span class='hljl-p'>(</span><span class='hljl-nf'>vbox</span><span class='hljl-p'>(</span><span class='hljl-n'>s1</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>s2</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>s3</span><span class='hljl-p'>),</span><span class='hljl-t'> </span><span class='hljl-nf'>vbox</span><span class='hljl-p'>(</span><span class='hljl-n'>scene1</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>scene2</span><span class='hljl-p'>),</span><span class='hljl-t'> </span><span class='hljl-n'>parent</span><span class='hljl-oB'>=</span><span class='hljl-n'>scene</span><span class='hljl-p'>)</span><span class='hljl-t'>
</span><span class='hljl-cs'># Do not execute beyond this point!</span><span class='hljl-t'>
</span><span class='hljl-nf'>RecordEvents</span><span class='hljl-p'>(</span><span class='hljl-n'>scene</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-s'>&quot;output&quot;</span><span class='hljl-p'>)</span><span class='hljl-t'>

</span>
</pre>

```
```@raw html

<div style="display:inline-block">
    <p style="display:inline-block; text-align: center">
        <video controls autoplay loop muted>
  <source src="http://juliaplots.org/MakieReferenceImages/gallery//ambient_occlusion/media/video.mp4" type="video/mp4">
  Your browser does not support mp4. Please use a modern browser like Chrome or Firefox.
</video>

    </p>
</div>

```