Requires_features(PLATOANALYZE_ENABLE_TPETRA)

# Name the test with the directory name
Plato_new_test(TEST_NAME)

# Copy Input files from source to binary dir
file( GLOB testFiles RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *.xml *.exo *.exodiff_commands *.sh)
Plato_add_test_files("${testFiles}")


# Set number of processors for PlatoMain comm
set( PLATOMAIN_NP 1 )

# Set number of processors for Performer comms
set( ANALYZE_NP 1 )

# Create list of comm sizes 
set( NUM_PROCS "${PLATOMAIN_NP} ${ANALYZE_NP}" )

# Specify which comm will provide the output for comparison
set( IO_COMM_INDEX 0 )

# Set the name of the interface file
set( INTERFACE_FILE interface.xml )

# Create the test and define the PlatoMain performer
set(APP_FILE platoApp.xml)
set(INPUT_FILE platoMain.xml)
Plato_create_test(PLATO_NEW_TEST ${PLATOMAIN_BINARY} ${PLATOMAIN_NP} ${INTERFACE_FILE} ${APP_FILE} ${INPUT_FILE})

# Define/add a performer
set( LOCAL_COMM_ID 1 )
set(APP_FILE analyzeApp.xml)
set(INPUT_FILE --input-config=analyzeInput.xml)
Plato_add_performer(PLATO_NEW_TEST ${ANALYZE_BINARY} ${ANALYZE_NP} ${LOCAL_COMM_ID} ${INTERFACE_FILE} ${APP_FILE} ${INPUT_FILE})

# Add the test
file( GLOB EXODIFF_COMMAND_FILE RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *.exodiff_commands)
file( GLOB EXODIFF_REFERENCE *.ref.exo )
set(INPUT_MESH bolted_bracket.exo)
set(OUTPUT_MESH platomain.exo.1.0)
Plato_add_test(${PLATO_NEW_TEST} ${TEST_NAME} ${NUM_PROCS} ${IO_COMM_INDEX} ${EXODIFF_COMMAND_FILE} ${EXODIFF_REFERENCE} ${INPUT_MESH} ${OUTPUT_MESH})
