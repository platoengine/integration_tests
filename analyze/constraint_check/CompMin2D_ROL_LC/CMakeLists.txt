Requires_features(PLATOANALYZE_ENABLE_PYTHON )

# Name the test with the directory name
Plato_new_test(TEST_NAME)

# Copy Input files from source to binary dir
set( testFiles "plato_input_deck.i;confirm_linearity.py")
Plato_add_test_files("${testFiles}")
Plato_analyze_copy_test_data("lbracket.exo")

# Set xml generator command
set(XMLGEN_COMMAND "XMLGenerator plato_input_deck.i")

# Set the name of the interface file
set( INTERFACE_FILE interface.xml )

# Set input file names for custom command
set( PYTHON_FILE "confirm_linearity.py")
set( RELATIVE_TOLERANCE 1e-11 )


SET(CUSTOM_COMMAND "python ${PYTHON_FILE} ${RELATIVE_TOLERANCE}")

# Add the test
Plato_add_xmlgen_custom_command_test(${TEST_NAME} ${XMLGEN_COMMAND} ${CUSTOM_COMMAND})

