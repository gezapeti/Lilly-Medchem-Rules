#Intel Compiler

#CXX = icpc
#CC = icc
#LD = icpc
#CXXFLAGS = -O2 -I . -I ../include -ffast-math -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64

CC=gcc
CXX = g++
LD = g++
CXXFLAGS = -O2 -I . -I ../include -ffast-math -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64

# Some versions of gcc need the -std= directive, remove if it causes problems
CXXFLAGS = -O2 -I . -I ../include -ffast-math -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 

# Auto check gcc version from Raj Guha
GCCVERSIONGTEQ4 := $(shell expr `gcc -dumpversion | cut -f1,2 -d.` \>= 4.3)
ifeq "$(GCCVERSIONGTEQ4)" "1"
    CXXFLAGS += -std=c++0x
endif


CP = cp


COMMON_OBJECTS = molecule.o moleculeb.o moleculeh.o element.o atom.o bond.o bond_list.o output.o ostream_and_type.o rmele.o etrans.o aromatic.o rwmolecule.o \
	smi.o mdl.o mdl_v30.o parse_smarts_tmp.o mdl_file_data.o mdl_molecule.o mdl_atom_record.o isis_link_atom.o ISIS_Atom_List.o atom_alias.o molecule_smarts.o\
	smiles.o smiles_support.o \
	moleculer.o pearlman.o moleculed.o path.o frag.o unique.o chiral_centre.o charge_assigner.o target.o careful_frag.o \
	iwrnm.o iwrcb.o set_of_atoms.o symm_class_can_rank.o ring_bond_iterator.o cis_trans_bond.o ematch.o coordinates.o dihedral.o\
	iwsubstructure.o csubstructure.o substructure_a.o substructure_env.o ss_atom_env.o ss_bonds.o ss_ring.o ss_ring_base.o ss_ring_sys.o iwqry_wstats.o substructure_results.o substructure_spec.o substructure_chiral.o\
	rwsubstructure.o substructure_nmab.o molecule_to_query.o is_actually_chiral.o tokenise_atomic_smarts.o temp_detach_atoms.o path_scoring.o \
	element_hits_needed.o misc2.o standardise.o toggle_kekule_form.o

MC_FIRST_PASS_OBJECTS = mc_first_pass.o $(COMMON_OBJECTS)

TSUBSTRUCTURE_OBJECTS = tsubstructure.o $(COMMON_OBJECTS)

IWDEMERIT_OBJECTS = iwdemerit.o substructure_demerits.o demerit.o $(COMMON_OBJECTS)

MC_SUMMARISE_OBJECTS = mc_summarise.o

EXECUTABLES = mc_first_pass tsubstructure iwdemerit mc_summarise

TSMILES_OBJECTS = tsmiles.o $(COMMON_OBJECTS)

all: $(EXECUTABLES)

install:  $(EXECUTABLES)
	if [ ! -d ../bin ] ; then mkdir ../bin ; fi
	$(CP) -p $(EXECUTABLES) ../bin

mc_first_pass: $(MC_FIRST_PASS_OBJECTS)
	$(LD) -o $@ $(MC_FIRST_PASS_OBJECTS) -L../lib/ -liwsupport -lz

tsubstructure: $(TSUBSTRUCTURE_OBJECTS)
	$(LD) -o $@ $(TSUBSTRUCTURE_OBJECTS) -L../lib/ -liwsupport -lz

iwdemerit: $(IWDEMERIT_OBJECTS)
	$(LD) -o $@ $(IWDEMERIT_OBJECTS) -L../lib/ -liwsupport -lz

mc_summarise: $(MC_SUMMARISE_OBJECTS)
	$(LD) -o $@ $(MC_SUMMARISE_OBJECTS) -L../lib/ -liwsupport -lz

tsmiles: $(TSMILES_OBJECTS)
	$(LD) -o $@ $(TSMILES_OBJECTS) -L../lib/ -liwsupport -lz

clean:
	-$(RM) $(COMMON_OBJECTS) mc_first_pass.o tsubstructure.o iwdemerit.o mc_summarise.o tsmiles.o substructure_demerits.o demerit.o $(EXECUTABLES)

uninstall:
	-$(RM) ../bin/tsubstructure ../bin/iwdemerit ../bin/mc_first_pass ../bin/mc_summarise
