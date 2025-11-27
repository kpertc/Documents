#python 

NumPy - multi-dimensional array

Why is NumPy faster? - Fixed Type

-   Faster to read less bytes of memory
-   No type checking when iterating through objects
-   Contiguous memory

<div style="display: grid; grid-template-columns: repeat(2, 2fr); grid-gap: 10px;">
	<div>
		Lists<br>
		 a = [1,3,5]<br>
		 b = [1,2,3]<br><br>
		 a*b=Error
	</div>
	<div>
		NumPy<br>
		a = np.array([1,3,5])<br>
		b = np.array([1,2,3])<br><br>
		a*b=np.array([1,6,15])
	</div>
</div>