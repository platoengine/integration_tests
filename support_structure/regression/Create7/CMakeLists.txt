Requires_features( STK_ENABLED )

Set_exodiff_files(EXODIFF_COMMAND_FILE EXODIFF_REFERENCE)
set( testFiles "input_mesh.exo" ${EXODIFF_COMMAND_FILE} ${EXODIFF_REFERENCE})
Plato_add_test_files( "${testFiles}" )

Plato_new_test(TEST_NAME)

set( TEST_COMMAND "mpirun -n 1 create_support_structure --input_mesh=input_mesh.exo --output_mesh=output_mesh.exo --design_field_name=density --build_plate_normal='0 1 0' --overhang_angle=30 --algorithm=5 --cell_size_multiplier=1 --neighbor_search_radius=2" )
set( OUTPUT_MESH "output_mesh.exo" )

Plato_add_serial_test( ${TEST_COMMAND} ${TEST_NAME} ${OUTPUT_MESH} ${EXODIFF_COMMAND_FILE} ${EXODIFF_REFERENCE} )
set_property(TEST ${TEST_NAME} PROPERTY LABELS "small")
