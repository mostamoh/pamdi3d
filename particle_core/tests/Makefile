FC 	:= mpif90
FFLAGS	:= -Wall -ffpe-trap=invalid,zero,overflow -g -O2 -fopenmp \
	-fcheck=array-temps,bounds,do,mem,pointer
TESTS	:= test_m_particle_core test_m_cross_sec

# Need these libraries for the tests
LIBS	:= particle_core
INCDIRS := ../src
LIBDIRS := ../src

%.o: 	%.f90
	$(FC) -c -o $@ $< $(FFLAGS) $(addprefix -I,$(INCDIRS))

%:	%.o
	$(FC) -o $@ $^ $(FFLAGS) $(addprefix -L,$(LIBDIRS)) $(addprefix -l,$(LIBS))

.PHONY: all clean

all: 	$(TESTS)

test:	$(TESTS)
	$(foreach test, $(TESTS), ./$(test);)

clean:
	$(RM) *.o *.mod $(TESTS)

# Dependencies
$(TESTS): ../src/libparticle_core.a
