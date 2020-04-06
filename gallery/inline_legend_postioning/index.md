## Inline legend postioning

```@raw html
<pre class='hljl'>
<span class='hljl-k'>using</span><span class='hljl-t'> </span><span class='hljl-n'>MakieLayout</span><span class='hljl-t'>
</span><span class='hljl-k'>using</span><span class='hljl-t'> </span><span class='hljl-n'>AbstractPlotting</span><span class='hljl-oB'>:</span><span class='hljl-t'> </span><span class='hljl-n'>px</span><span class='hljl-t'>

</span><span class='hljl-k'>using</span><span class='hljl-t'> </span><span class='hljl-n'>AbstractPlotting</span><span class='hljl-t'>

</span><span class='hljl-n'>haligns</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-p'>[</span><span class='hljl-sc'>:left</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-sc'>:right</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-sc'>:center</span><span class='hljl-p'>]</span><span class='hljl-t'>
</span><span class='hljl-n'>valigns</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-p'>[</span><span class='hljl-sc'>:top</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-sc'>:bottom</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-sc'>:center</span><span class='hljl-p'>]</span><span class='hljl-t'>

</span><span class='hljl-n'>scene</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>layout</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>layoutscene</span><span class='hljl-p'>(</span><span class='hljl-n'>resolution</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-p'>(</span><span class='hljl-ni'>1400</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-ni'>900</span><span class='hljl-p'>))</span><span class='hljl-t'>

</span><span class='hljl-n'>ax</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-n'>layout</span><span class='hljl-p'>[</span><span class='hljl-ni'>1</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-ni'>1</span><span class='hljl-p'>]</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>LAxis</span><span class='hljl-p'>(</span><span class='hljl-n'>scene</span><span class='hljl-p'>)</span><span class='hljl-t'>

</span><span class='hljl-n'>xs</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-ni'>0</span><span class='hljl-oB'>:</span><span class='hljl-nfB'>0.1</span><span class='hljl-oB'>:</span><span class='hljl-ni'>10</span><span class='hljl-t'>
</span><span class='hljl-n'>lins</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-p'>[</span><span class='hljl-nf'>lines!</span><span class='hljl-p'>(</span><span class='hljl-n'>ax</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>xs</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>sin</span><span class='hljl-oB'>.</span><span class='hljl-p'>(</span><span class='hljl-n'>xs</span><span class='hljl-t'> </span><span class='hljl-oB'>.*</span><span class='hljl-t'> </span><span class='hljl-n'>i</span><span class='hljl-p'>),</span><span class='hljl-t'> </span><span class='hljl-n'>color</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-n'>color</span><span class='hljl-p'>)</span><span class='hljl-t'>
    </span><span class='hljl-k'>for</span><span class='hljl-t'> </span><span class='hljl-p'>(</span><span class='hljl-n'>i</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>color</span><span class='hljl-p'>)</span><span class='hljl-t'> </span><span class='hljl-kp'>in</span><span class='hljl-t'> </span><span class='hljl-nf'>zip</span><span class='hljl-p'>(</span><span class='hljl-ni'>1</span><span class='hljl-oB'>:</span><span class='hljl-ni'>3</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-p'>[</span><span class='hljl-sc'>:red</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-sc'>:blue</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-sc'>:green</span><span class='hljl-p'>])]</span><span class='hljl-t'>

</span><span class='hljl-n'>legends</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-p'>[</span><span class='hljl-nf'>LLegend</span><span class='hljl-p'>(</span><span class='hljl-t'>
        </span><span class='hljl-n'>scene</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>lins</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-p'>[</span><span class='hljl-s'>&quot;Line </span><span class='hljl-si'>$i</span><span class='hljl-s'>&quot;</span><span class='hljl-t'> </span><span class='hljl-k'>for</span><span class='hljl-t'> </span><span class='hljl-n'>i</span><span class='hljl-t'> </span><span class='hljl-kp'>in</span><span class='hljl-t'> </span><span class='hljl-ni'>1</span><span class='hljl-oB'>:</span><span class='hljl-ni'>3</span><span class='hljl-p'>],</span><span class='hljl-t'>
        </span><span class='hljl-s'>&quot;</span><span class='hljl-si'>$ha</span><span class='hljl-s'> &amp; </span><span class='hljl-si'>$va</span><span class='hljl-s'>&quot;</span><span class='hljl-p'>,</span><span class='hljl-t'>
        </span><span class='hljl-n'>width</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-nf'>Auto</span><span class='hljl-p'>(</span><span class='hljl-kc'>false</span><span class='hljl-p'>),</span><span class='hljl-t'>
        </span><span class='hljl-n'>margin</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-p'>(</span><span class='hljl-ni'>10</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-ni'>10</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-ni'>10</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-ni'>10</span><span class='hljl-p'>),</span><span class='hljl-t'>
        </span><span class='hljl-n'>halign</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-n'>ha</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>valign</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-n'>va</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>orientation</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-sc'>:horizontal</span><span class='hljl-t'>
    </span><span class='hljl-p'>)</span><span class='hljl-t'> </span><span class='hljl-k'>for</span><span class='hljl-t'> </span><span class='hljl-p'>(</span><span class='hljl-n'>j</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>ha</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>va</span><span class='hljl-p'>)</span><span class='hljl-t'> </span><span class='hljl-kp'>in</span><span class='hljl-t'> </span><span class='hljl-nf'>zip</span><span class='hljl-p'>(</span><span class='hljl-ni'>1</span><span class='hljl-oB'>:</span><span class='hljl-ni'>3</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>haligns</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-n'>valigns</span><span class='hljl-p'>)]</span><span class='hljl-t'>


</span><span class='hljl-k'>for</span><span class='hljl-t'> </span><span class='hljl-n'>leg</span><span class='hljl-t'> </span><span class='hljl-kp'>in</span><span class='hljl-t'> </span><span class='hljl-n'>legends</span><span class='hljl-t'>
    </span><span class='hljl-n'>layout</span><span class='hljl-p'>[</span><span class='hljl-ni'>1</span><span class='hljl-p'>,</span><span class='hljl-t'> </span><span class='hljl-ni'>1</span><span class='hljl-p'>]</span><span class='hljl-t'> </span><span class='hljl-oB'>=</span><span class='hljl-t'> </span><span class='hljl-n'>leg</span><span class='hljl-t'>
</span><span class='hljl-k'>end</span><span class='hljl-t'>   

</span><span class='hljl-n'>scene</span><span class='hljl-t'>

</span>
</pre>

```
```@raw html

<div style="display:inline-block">
    <p style="display:inline-block; text-align: center">
        <img src="http://juliaplots.org/MakieReferenceImages/gallery//inline_legend_postioning/media/image.jpg" alt="">

    </p>
</div>

```