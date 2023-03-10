Requires_features( PLATOANALYZE_PE_SERVICES PLATOANALYZE_ENABLE_ESP )

# Name the test with the directory name
Plato_new_test(TEST_NAME)

# Copy Input files from source to binary dir
set( testFiles "plato_input_deck.i;rocker.csm;compute_infinity_norm.py;surrogate_based_global_optim_dakota.dat.gold")
Plato_add_test_files("${testFiles}")

# Set xml generator command
set(XMLGEN_COMMAND "XMLGenerator plato_input_deck.i")

# Set the name of the interface file
set( INTERFACE_FILE interface.xml )

# Set input file names for custom command
set( PYTHON_FILE "compute_infinity_norm.py")
set( INFNORM_IGNORE_ROWS 12 )
set( INFNORM_RELATIVE_TOLERANCE 1e-2 )
set( OUT_FILE "dakota_surrogate_based_global_optimization.dat")
set( GOLD_FILE "surrogate_based_global_optim_dakota.dat.gold")

SET(CUSTOM_COMMAND "python ${PYTHON_FILE} ${INFNORM_IGNORE_ROWS} ${INFNORM_RELATIVE_TOLERANCE} ${OUT_FILE} ${CMAKE_CURRENT_SOURCE_DIR}/${GOLD_FILE}")

# Add the test
Plato_add_xmlgen_custom_command_test(${TEST_NAME} ${XMLGEN_COMMAND} ${CUSTOM_COMMAND})

