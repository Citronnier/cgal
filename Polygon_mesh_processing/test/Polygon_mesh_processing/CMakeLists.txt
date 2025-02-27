# Created by the script cgal_create_CMakeLists
# This is the CMake script for compiling a set of CGAL applications.

cmake_minimum_required(VERSION 3.1...3.20)
project(Polygon_mesh_processing_Tests)

# CGAL and its components
find_package(CGAL REQUIRED COMPONENTS Core)

include(${CGAL_USE_FILE})

# Boost and its components
find_package(Boost REQUIRED)

if(NOT Boost_FOUND)

  message(
    STATUS "This project requires the Boost library, and will not be compiled.")

  return()

endif()

# include for local directory

# include for local package
find_package(Eigen3 3.2.0) #(requires 3.2.0 or greater)
include(CGAL_Eigen3_support)

find_package(TBB)
include(CGAL_TBB_support)

if(TARGET CGAL::Eigen3_support)
  # Creating entries for all .cpp/.C files with "main" routine
  # ##########################################################
  create_single_source_cgal_program("fairing_test.cpp")
  target_link_libraries(fairing_test PUBLIC CGAL::Eigen3_support)
  create_single_source_cgal_program(
    "triangulate_hole_Polyhedron_3_no_delaunay_test.cpp")
  target_link_libraries(triangulate_hole_Polyhedron_3_no_delaunay_test
                        PUBLIC CGAL::Eigen3_support)
  create_single_source_cgal_program("triangulate_hole_Polyhedron_3_test.cpp")
  target_link_libraries(triangulate_hole_Polyhedron_3_test
                        PUBLIC CGAL::Eigen3_support)
  create_single_source_cgal_program("test_shape_smoothing.cpp")
  target_link_libraries(test_shape_smoothing PUBLIC CGAL::Eigen3_support)

endif()

find_package(OpenMesh QUIET)
if(OpenMesh_FOUND)
  include(UseOpenMesh)
else()
  message(STATUS "Examples that use OpenMesh will not be compiled.")
endif()

create_single_source_cgal_program("test_hausdorff_bounded_error_distance.cpp")
create_single_source_cgal_program("test_pmp_read_polygon_mesh.cpp")
create_single_source_cgal_program("connected_component_polyhedron.cpp")
create_single_source_cgal_program("connected_component_surface_mesh.cpp")
create_single_source_cgal_program("test_detect_features.cpp")
create_single_source_cgal_program("pmp_compute_normals_test.cpp")
create_single_source_cgal_program("orient_polygon_mesh_test.cpp")
create_single_source_cgal_program("orient_polygon_soup_test.cpp")
create_single_source_cgal_program("point_inside_polyhedron_boundary_test.cpp")
create_single_source_cgal_program("point_inside_surface_mesh_test.cpp")
create_single_source_cgal_program("polygon_mesh_slicer_test.cpp")
create_single_source_cgal_program("self_intersection_polyhedron_test.cpp")
create_single_source_cgal_program("self_intersection_surface_mesh_test.cpp")
create_single_source_cgal_program("pmp_do_intersect_test.cpp")
create_single_source_cgal_program("test_is_polygon_soup_a_polygon_mesh.cpp")
create_single_source_cgal_program("test_stitching.cpp")
create_single_source_cgal_program("remeshing_test.cpp")
create_single_source_cgal_program("remeshing_with_isolated_constraints_test.cpp" )
create_single_source_cgal_program("measures_test.cpp")
create_single_source_cgal_program("triangulate_faces_test.cpp")
create_single_source_cgal_program("triangulate_faces_hole_filling_dt3_test.cpp")
create_single_source_cgal_program("triangulate_faces_hole_filling_all_search_test.cpp")
create_single_source_cgal_program("test_pmp_remove_border_edge.cpp")
create_single_source_cgal_program("test_pmp_distance.cpp")
create_single_source_cgal_program("test_corefinement_and_constraints.cpp")
create_single_source_cgal_program("test_corefinement_and_constraints_nearest.cpp")
create_single_source_cgal_program("test_corefinement_bool_op.cpp")
create_single_source_cgal_program("test_corefine.cpp")
create_single_source_cgal_program("test_coref_epic_points_identity.cpp")
create_single_source_cgal_program("test_does_bound_a_volume.cpp")
create_single_source_cgal_program("test_pmp_clip.cpp")
create_single_source_cgal_program("test_autorefinement.cpp")
create_single_source_cgal_program("autorefinement_sm.cpp")
create_single_source_cgal_program( "corefine_non_manifold.cpp" )
create_single_source_cgal_program("triangulate_hole_polyline_test.cpp")
create_single_source_cgal_program("surface_intersection_sm_poly.cpp")
create_single_source_cgal_program("test_orient_cc.cpp")
create_single_source_cgal_program("test_pmp_transform.cpp")
create_single_source_cgal_program("extrude_test.cpp")
create_single_source_cgal_program("test_split_volume.cpp")
create_single_source_cgal_program("test_merging_border_vertices.cpp")
create_single_source_cgal_program("test_repair_polygon_soup.cpp")
create_single_source_cgal_program("test_shape_predicates.cpp")
create_single_source_cgal_program("test_pmp_collision_detection.cpp")
create_single_source_cgal_program("test_pmp_locate.cpp")
create_single_source_cgal_program("test_pmp_snapping.cpp")
create_single_source_cgal_program("test_pmp_non_conforming_snapping.cpp")
create_single_source_cgal_program("test_pmp_repair_degeneracies.cpp")
create_single_source_cgal_program("test_pmp_manifoldness.cpp")
create_single_source_cgal_program("test_mesh_smoothing.cpp")
create_single_source_cgal_program("test_remove_caps_needles.cpp")
create_single_source_cgal_program("test_simplify_polylines_pmp.cpp")
create_single_source_cgal_program("triangulate_hole_with_cdt_2_test.cpp")
create_single_source_cgal_program("test_pmp_polyhedral_envelope.cpp")
#  create_single_source_cgal_program("test_pmp_repair_self_intersections.cpp")

find_package(METIS)
include(CGAL_METIS_support)
if(TARGET CGAL::METIS_support)
  target_link_libraries(test_hausdorff_bounded_error_distance PUBLIC CGAL::METIS_support)
else()
  message(STATUS "Tests, which use the METIS library will not be compiled.")
endif()

if(TARGET CGAL::TBB_support)
  target_link_libraries(test_hausdorff_bounded_error_distance PUBLIC CGAL::TBB_support)
  target_link_libraries(test_pmp_distance PUBLIC CGAL::TBB_support)
  target_link_libraries(orient_polygon_soup_test PUBLIC CGAL::TBB_support)
  target_link_libraries(self_intersection_surface_mesh_test
                        PUBLIC CGAL::TBB_support)
else()
  message(
    STATUS
      "NOTICE: Intel TBB was not found. test_pmp_distance will use sequential code."
  )
endif()

if(OpenMesh_FOUND)
  create_single_source_cgal_program("remeshing_test_P_SM_OM.cpp")
  target_link_libraries(remeshing_test_P_SM_OM PRIVATE ${OPENMESH_LIBRARIES})
endif()

find_package(Ceres QUIET)
include(CGAL_Ceres_support)

if(TARGET CGAL::Ceres_support AND TARGET CGAL::Eigen3_support)
  target_link_libraries( test_mesh_smoothing PUBLIC CGAL::Eigen3_support CGAL::Ceres_support)

#  target_compile_definitions( test_pmp_repair_self_intersections PRIVATE CGAL_PMP_USE_CERES_SOLVER )
#  target_link_libraries( test_pmp_repair_self_intersections PRIVATE ceres )
endif(TARGET CGAL::Ceres_support AND TARGET CGAL::Eigen3_support)

if(BUILD_TESTING)
  set_tests_properties(
    execution___of__triangulate_hole_Polyhedron_3_no_delaunay_test
    execution___of__triangulate_hole_Polyhedron_3_test
    PROPERTIES RESOURCE_LOCK Triangulation_with_hole)
endif()
