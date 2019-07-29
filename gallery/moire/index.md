## Moire

```@raw html
<pre class='hljl'>
<span class='hljl-k'>using</span><span class='hljl-t'> </span><span class='hljl-n'>Makie</span><span class='hljl-t'>

 </span><span class='hljl-k'>function</span><span class='hljl-t'> </span><span class='hljl-nf'>cartesian</span><span class='hljl-p'>(</span><span class='hljl-n'>ll</span><span class='hljl-p'>)</span><span class='hljl-t'>
     </span><span class='hljl-k'>return</span><span class='hljl-t'> </span><span class='hljl-nf'>Point3f0</span><span class='hljl-p'>(</span><span class='hljl-t'>
         </span><span class='hljl-nf'>cos</span><span class='hljl-p'>(</span><span class='hljl-n'>ll</span><span class='hljl-p'>[</span><span class='hljl-ni'>1</span><span class='hljl-p'>])</span><span class='hljl-t'> </span><span class='hljl-oB'>*</span><span class='hljl-t'> </span><span class='hljl-nf'>sin</span><span class='hljl-p'>(</span><span class='hljl-n'>ll</span><span class='hljl-p'>[</span><span class='hljl-ni'>2</span><span class='hljl-p'>]),</span><span class='hljl-t'>
         </span><span class='hljl-nf'>sin</span><span class='hljl-p'>(</span><span class='hljl-n'>ll</span><span class='hljl-p'>[</span><span class='hljl-ni'>1</span><span class='hljl-p'>])</span><span class='hljl-t'> </span><span class='hljl-oB'>*</span><span class='hljl-t'> </span><span class='hljl-nf'>sin</span><span class='hljl-p'>(</span><span class='hljl-n'>ll</span><span class='hljl-p'>[</span><span class='hljl-ni'>2</span><span class='hljl-p'>]),</span><span class='hljl-t'>
         </span><span class='hljl-nf'>cos</span><span class='hljl-p'>(</span><span class='hljl-n'>ll</span><span class='hljl-p'>[</span><span class='hljl-ni'>2</span><span class='hljl-p'>])</span><span class='hljl-t'>
     </span><span class='hljl-p'>)</span><span class='hljl-t'>
 </span><span class='hljl-k'>end</span><span class='hljl-t'>
 </span><span class='hljl-nf'>fract</span><span class='hljl-p'>(</span><span class='hljl-n'>x</span><span class='hljl-p'>)</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-n'>x</span><span class='hljl-t'> </span><span class='hljl-oB'>-</span><span class='hljl-t'> </span><span class='hljl-nf'>floor</span><span class='hljl-p'>(</span><span class='hljl-n'>x</span><span class='hljl-p'>)</span><span class='hljl-t'>
 </span><span class='hljl-k'>function</span><span class='hljl-t'> </span><span class='hljl-nf'>calcpositions</span><span class='hljl-p'>(</span><span class='hljl-n'>rings</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>index</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>time</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>audio</span><span class='hljl-p'>)</span><span class='hljl-t'>
     </span><span class='hljl-n'>movement</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>radius</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>speed</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>spin</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-ni'>1</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-ni'>2</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-ni'>3</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-ni'>4</span><span class='hljl-p'>;</span><span class='hljl-t'>
     </span><span class='hljl-n'>position</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>Point3f0</span><span class='hljl-p'>(</span><span class='hljl-nfB'>0.0</span><span class='hljl-p'>)</span><span class='hljl-t'>
     </span><span class='hljl-n'>precision</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.2f0</span><span class='hljl-t'>
     </span><span class='hljl-k'>for</span><span class='hljl-t'> </span><span class='hljl-n'>ring</span><span class='hljl-t'> </span><span class='hljl-kp'>in</span><span class='hljl-t'> </span><span class='hljl-n'>rings</span><span class='hljl-t'>
         </span><span class='hljl-n'>position</span><span class='hljl-t'> </span><span class='hljl-oB'>+=</span><span class='hljl-t'> </span><span class='hljl-n'>ring</span><span class='hljl-p'>[</span><span class='hljl-n'>radius</span><span class='hljl-p'>]</span><span class='hljl-t'> </span><span class='hljl-oB'>*</span><span class='hljl-t'> </span><span class='hljl-nf'>cartesian</span><span class='hljl-p'>(</span><span class='hljl-t'>
             </span><span class='hljl-n'>precision</span><span class='hljl-t'> </span><span class='hljl-oB'>*</span><span class='hljl-t'>
             </span><span class='hljl-n'>index</span><span class='hljl-t'> </span><span class='hljl-oB'>*</span><span class='hljl-t'>
             </span><span class='hljl-nf'>Point2f0</span><span class='hljl-p'>(</span><span class='hljl-n'>ring</span><span class='hljl-p'>[</span><span class='hljl-n'>spin</span><span class='hljl-p'>]</span><span class='hljl-t'> </span><span class='hljl-oB'>+</span><span class='hljl-t'> </span><span class='hljl-nf'>Point2f0</span><span class='hljl-p'>(</span><span class='hljl-nf'>sin</span><span class='hljl-p'>(</span><span class='hljl-n'>time</span><span class='hljl-t'> </span><span class='hljl-oB'>*</span><span class='hljl-t'> </span><span class='hljl-n'>ring</span><span class='hljl-p'>[</span><span class='hljl-n'>speed</span><span class='hljl-p'>]),</span><span class='hljl-t'> </span><span class='hljl-nf'>cos</span><span class='hljl-p'>(</span><span class='hljl-n'>time</span><span class='hljl-t'> </span><span class='hljl-oB'>*</span><span class='hljl-t'> </span><span class='hljl-n'>ring</span><span class='hljl-p'>[</span><span class='hljl-n'>speed</span><span class='hljl-p'>]))</span><span class='hljl-t'> </span><span class='hljl-oB'>*</span><span class='hljl-t'> </span><span class='hljl-n'>ring</span><span class='hljl-p'>[</span><span class='hljl-n'>movement</span><span class='hljl-p'>])</span><span class='hljl-t'>
         </span><span class='hljl-p'>)</span><span class='hljl-t'>
     </span><span class='hljl-k'>end</span><span class='hljl-t'>
     </span><span class='hljl-n'>amplitude</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-n'>audio</span><span class='hljl-p'>[</span><span class='hljl-nf'>round</span><span class='hljl-p'>(</span><span class='hljl-n'>Int</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nf'>clamp</span><span class='hljl-p'>(</span><span class='hljl-nf'>fract</span><span class='hljl-p'>(</span><span class='hljl-n'>position</span><span class='hljl-p'>[</span><span class='hljl-ni'>1</span><span class='hljl-p'>]</span><span class='hljl-t'> </span><span class='hljl-oB'>*</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.1</span><span class='hljl-p'>),</span><span class='hljl-t'> </span><span class='hljl-ni'>0</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-ni'>1</span><span class='hljl-p'>)</span><span class='hljl-t'> </span><span class='hljl-oB'>*</span><span class='hljl-t'> </span><span class='hljl-p'>(</span><span class='hljl-ni'>25000</span><span class='hljl-oB'>-</span><span class='hljl-ni'>1</span><span class='hljl-p'>))</span><span class='hljl-t'> </span><span class='hljl-oB'>+</span><span class='hljl-t'> </span><span class='hljl-ni'>1</span><span class='hljl-p'>];</span><span class='hljl-t'> </span><span class='hljl-cs'># index * 0.002</span><span class='hljl-t'>
     </span><span class='hljl-n'>position</span><span class='hljl-t'> </span><span class='hljl-oB'>*=</span><span class='hljl-t'> </span><span class='hljl-nfB'>1.0</span><span class='hljl-t'> </span><span class='hljl-oB'>+</span><span class='hljl-t'> </span><span class='hljl-n'>amplitude</span><span class='hljl-t'> </span><span class='hljl-oB'>*</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.5</span><span class='hljl-p'>;</span><span class='hljl-t'>
     </span><span class='hljl-n'>position</span><span class='hljl-t'>
 </span><span class='hljl-k'>end</span><span class='hljl-t'>
 </span><span class='hljl-n'>rings</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-p'>[(</span><span class='hljl-nfB'>0.1f0</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>1.0f0</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.00001f0</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nf'>Point2f0</span><span class='hljl-p'>(</span><span class='hljl-nfB'>0.2</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.1</span><span class='hljl-p'>)),</span><span class='hljl-t'> </span><span class='hljl-p'>(</span><span class='hljl-nfB'>0.1f0</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.0f0</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.0002f0</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nf'>Point2f0</span><span class='hljl-p'>(</span><span class='hljl-nfB'>0.052</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.05</span><span class='hljl-p'>))]</span><span class='hljl-t'>
 </span><span class='hljl-n'>N2</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-ni'>25000</span><span class='hljl-t'>
 </span><span class='hljl-n'>t_audio</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-n'>sin</span><span class='hljl-oB'>.</span><span class='hljl-p'>(</span><span class='hljl-nf'>range</span><span class='hljl-p'>(</span><span class='hljl-ni'>0</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>stop</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-ni'>10</span><span class='hljl-n'>pi</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>length</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-n'>N2</span><span class='hljl-p'>))</span><span class='hljl-t'> </span><span class='hljl-oB'>.+</span><span class='hljl-t'> </span><span class='hljl-p'>(</span><span class='hljl-n'>cos</span><span class='hljl-oB'>.</span><span class='hljl-p'>(</span><span class='hljl-nf'>range</span><span class='hljl-p'>(</span><span class='hljl-oB'>-</span><span class='hljl-ni'>3</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>stop</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-ni'>7</span><span class='hljl-n'>pi</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>length</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-n'>N2</span><span class='hljl-p'>))</span><span class='hljl-t'> </span><span class='hljl-oB'>.*</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.6</span><span class='hljl-p'>)</span><span class='hljl-t'> </span><span class='hljl-oB'>.+</span><span class='hljl-t'> </span><span class='hljl-p'>(</span><span class='hljl-nf'>rand</span><span class='hljl-p'>(</span><span class='hljl-n'>Float32</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>N2</span><span class='hljl-p'>)</span><span class='hljl-t'> </span><span class='hljl-oB'>.*</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.1</span><span class='hljl-p'>)</span><span class='hljl-t'> </span><span class='hljl-oB'>./</span><span class='hljl-t'> </span><span class='hljl-nfB'>2f0</span><span class='hljl-t'>
 </span><span class='hljl-n'>start</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>time</span><span class='hljl-p'>()</span><span class='hljl-t'>
 </span><span class='hljl-n'>t</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-p'>(</span><span class='hljl-nf'>time</span><span class='hljl-p'>()</span><span class='hljl-t'> </span><span class='hljl-oB'>-</span><span class='hljl-t'> </span><span class='hljl-n'>start</span><span class='hljl-p'>)</span><span class='hljl-t'> </span><span class='hljl-oB'>*</span><span class='hljl-t'> </span><span class='hljl-ni'>100</span><span class='hljl-t'>
 </span><span class='hljl-n'>pos</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-n'>calcpositions</span><span class='hljl-oB'>.</span><span class='hljl-p'>((</span><span class='hljl-n'>rings</span><span class='hljl-p'>,),</span><span class='hljl-t'> </span><span class='hljl-ni'>1</span><span class='hljl-oB'>:</span><span class='hljl-n'>N2</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>t</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-p'>(</span><span class='hljl-n'>t_audio</span><span class='hljl-p'>,))</span><span class='hljl-t'>

 </span><span class='hljl-n'>scene</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>lines</span><span class='hljl-p'>(</span><span class='hljl-t'>
     </span><span class='hljl-n'>pos</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>color</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-n'>RGBAf0</span><span class='hljl-oB'>.</span><span class='hljl-p'>(</span><span class='hljl-nf'>to_colormap</span><span class='hljl-p'>(</span><span class='hljl-sc'>:RdBu</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>N2</span><span class='hljl-p'>),</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.6</span><span class='hljl-p'>),</span><span class='hljl-t'>
     </span><span class='hljl-n'>thickness</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.6f0</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>show_axis</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-kc'>false</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>transparency</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-kc'>true</span><span class='hljl-t'>
 </span><span class='hljl-p'>)</span><span class='hljl-t'>
 </span><span class='hljl-nf'>linesegments!</span><span class='hljl-p'>(</span><span class='hljl-t'>
     </span><span class='hljl-n'>scene</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nf'>FRect3D</span><span class='hljl-p'>(</span><span class='hljl-nf'>Vec3f0</span><span class='hljl-p'>(</span><span class='hljl-oB'>-</span><span class='hljl-nfB'>1.5</span><span class='hljl-p'>),</span><span class='hljl-t'> </span><span class='hljl-nf'>Vec3f0</span><span class='hljl-p'>(</span><span class='hljl-ni'>3</span><span class='hljl-p'>)),</span><span class='hljl-t'> </span><span class='hljl-n'>raw</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-kc'>true</span><span class='hljl-p'>,</span><span class='hljl-t'>
     </span><span class='hljl-n'>linewidth</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-ni'>3</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>linestyle</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-sc'>:dot</span><span class='hljl-t'>
 </span><span class='hljl-p'>)</span><span class='hljl-t'>
 </span><span class='hljl-n'>eyepos</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>Vec3f0</span><span class='hljl-p'>(</span><span class='hljl-ni'>5</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>1.5</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.5</span><span class='hljl-p'>)</span><span class='hljl-t'>
 </span><span class='hljl-n'>lookat</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>Vec3f0</span><span class='hljl-p'>(</span><span class='hljl-ni'>0</span><span class='hljl-p'>)</span><span class='hljl-t'>
 </span><span class='hljl-nf'>update_cam!</span><span class='hljl-p'>(</span><span class='hljl-n'>scene</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>eyepos</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>lookat</span><span class='hljl-p'>)</span><span class='hljl-t'>
 </span><span class='hljl-n'>scene</span><span class='hljl-oB'>.</span><span class='hljl-n'>center</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-kc'>false</span><span class='hljl-t'> </span><span class='hljl-cs'># prevent scene from recentering on display</span><span class='hljl-t'>
 </span><span class='hljl-n'>l</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-n'>scene</span><span class='hljl-p'>[</span><span class='hljl-ni'>1</span><span class='hljl-p'>]</span><span class='hljl-t'>
 </span><span class='hljl-n'>N</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-ni'>150</span><span class='hljl-t'>
 </span><span class='hljl-nf'>record</span><span class='hljl-p'>(</span><span class='hljl-n'>scene</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-s'>&quot;output.mp4&quot;</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-ni'>1</span><span class='hljl-oB'>:</span><span class='hljl-n'>N</span><span class='hljl-p'>)</span><span class='hljl-t'> </span><span class='hljl-k'>do</span><span class='hljl-t'> </span><span class='hljl-n'>i</span><span class='hljl-t'>
     </span><span class='hljl-n'>t</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-p'>(</span><span class='hljl-nf'>time</span><span class='hljl-p'>()</span><span class='hljl-t'> </span><span class='hljl-oB'>-</span><span class='hljl-t'> </span><span class='hljl-n'>start</span><span class='hljl-p'>)</span><span class='hljl-t'> </span><span class='hljl-oB'>*</span><span class='hljl-t'> </span><span class='hljl-ni'>700</span><span class='hljl-t'>
     </span><span class='hljl-n'>pos</span><span class='hljl-t'> </span><span class='hljl-oB'>.=</span><span class='hljl-t'> </span><span class='hljl-n'>calcpositions</span><span class='hljl-oB'>.</span><span class='hljl-p'>((</span><span class='hljl-n'>rings</span><span class='hljl-p'>,),</span><span class='hljl-t'> </span><span class='hljl-ni'>1</span><span class='hljl-oB'>:</span><span class='hljl-n'>N2</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>t</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-p'>(</span><span class='hljl-n'>t_audio</span><span class='hljl-p'>,))</span><span class='hljl-t'>
     </span><span class='hljl-n'>l</span><span class='hljl-p'>[</span><span class='hljl-ni'>1</span><span class='hljl-p'>]</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-n'>pos</span><span class='hljl-t'> </span><span class='hljl-cs'># update argument 1</span><span class='hljl-t'>
     </span><span class='hljl-nf'>rotate_cam!</span><span class='hljl-p'>(</span><span class='hljl-n'>scene</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.0</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.01</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-nfB'>0.01</span><span class='hljl-p'>)</span><span class='hljl-t'>
</span><span class='hljl-k'>end</span><span class='hljl-t'>

</span>
</pre>

```
```@raw html

<div style="display:inline-block">
    <p style="display:inline-block; text-align: center">
        <video controls autoplay loop muted>
  <source src="https://simondanisch.github.io/ReferenceImages/gallery//moire/media/moire.mp4" type="video/mp4">
  Your browser does not support mp4. Please use a modern browser like Chrome or Firefox.
</video>

    </p>
</div>

```