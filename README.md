# NumaAllocator

This *very* simple code is a C++ allocator that gives some control
over where C++ containers allocate memory.

In a multithreaded code it is often enough to rely on the OS
first touch policy to achieve this implicitly, but sometimes
the different memory "nodes" can have wildly
different performance characteristics requiring programmer
to take more control.


#Dependencies

This simple include-only library does depend
on [libnuma](http://oss.sgi.com/projects/libnuma/).
You will need numa.h header file as well as 
a [shared] object file to link against.


# Example



```c++

#include <vector>
#include "numaalloc.h"
int main(int argc,char** argv){

  int n1=0;
  int n2=1;
  int sz=5000;

  typedef NumaAlloc::NumaAlloc<float> na_t;


  //Allocate vector of floats bound to numa node n1
  std::vector<float,na_t > x(sz,0.0,na_t(n1));

  //Allocate vector of floats bound to numa node n2
  std::vector<float,na_t > y(sz,0.0,na_t(n2));


  //Do something with x,y in parallel for win.




  return 0;

}


```
