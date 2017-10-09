Copy the contents of file [`MMult_4x4_12.c`](../blob/master/src/MMult_4x4_12.c) into a file named [`MMult_4x4_13.c`](../blob/master/src/MMult_4x4_13.c) and change the contents:

Change the first lines in the `makefile` to
```makefile
OLD  := MMult_4x4_12
NEW  := MMult_4x4_13
```
 * `make run`
```matlab
octave:3> PlotAll        % this will create the plot
```

This time the performance graph will look something like

![](../raw/master/figures/compare_MMult-4x4-12_MMult-4x4-13.png)


This version saves the packed blocks of A so that after the first iteration of the outer loop of `InnerKernel`, the saved version is used.  The performance gain is noticeable!  The only change from the last version is the addition of `if ( j== 0 )`:
```c
      if ( j == 0 ) PackMatrixA( k, &A( i, 0 ), lda, &packedA[ i*k ] );
```

