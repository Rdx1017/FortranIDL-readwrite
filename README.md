#FORTRAN(write) AND IDL(read)

I prefer to let file access = 'Sequential',so all files are sequential.

In this paper, i will try 'formatted' and 'unformatted' to send data.

##FORMATTED

FORTRAN CODE

```
Program main

  Implicit none
  Integer arr(3,5),i

  Do i = 0,14
    arr(mod(i,3)+1,i/3+1) = i
  End do

  Open(1,file = 'hello')

  Write(1,*)arr

  close(1)

End Program

```

IDL CODE

```
pro readnewarr

  openr,lun,'hello',/get_lun

  arr = Intarr(3,5)

  ;while(~eof(lun))do begin
  ;  readf,lun,tmp
  ;Endwhile
  ;print,tmp

  Readf,lun,arr

  print,arr

end

```
>We can find,if difine an array(m,n) in fortran,
it means the array has m rows and n columns,
and the array was saved by column.

>Then,in idl if you want to read this array,
just use array(m,n),but it was saved by row.

If you want to use 'unformatted',just add:

>Open(1,file = 'newarr',access = 'sequential', form = 'unformatted')

and

>  Write(1)arr

in fortran code.

and in idl,use:

>openr,lun,'hello',/get_lun,/f77_unformatted

and use:

>readu,lun,arr
