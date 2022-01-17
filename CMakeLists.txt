cmake_minimum_required(VERSION 3.12.0)
project(Fast_LDPC_decoder_for_x86)
include(CTest)

set(SOURCES
    src/CBitGenerator/CBitGenerator.cpp
    src/CChanel/CChanel.cpp
    src/CChanel/CChanelAWGN_MKL.cpp
    src/CDecoder/template/CDecoder.cpp
    src/CDecoder/template/CDecoder_fixed.cpp
    src/CDecoder/template/CDecoder_fixed_AVX.cpp
    src/CDecoder/template/CDecoder_fixed_SSE.cpp
    src/CDecoder/OMS/CDecoder_OMS_fixed_SSE.cpp
    src/CDecoder/OMS/CDecoder_OMS_fixed_AVX.cpp
    src/CDecoder/NMS/CDecoder_NMS_fixed_SSE.cpp
    src/CDecoder/NMS/CDecoder_NMS_fixed_AVX.cpp
    src/CEncoder/CFakeEncoder.cpp
    src/CEncoder/Encoder.cpp
    src/CEncoder/GenericEncoder.cpp
    src/CErrorAnalyzer/CErrorAnalyzer.cpp
    src/CFixPointConversion/CFastFixConversion.cpp
    src/CFixPointConversion/CFixConversion.cpp
    src/CTerminal/CTerminal.cpp
    src/CTimer/CTimer.cpp
    src/CTools/CTools.cpp
    src/CTools/transpose_avx.cpp
    src/CTrame/CTrame.cpp
    src/main_p.cpp)

add_executable(${PROJECT_NAME} ${SOURCES})

set(CMAKE_CXX_FLAGS
    "${CMAKE_CXX_FLAGS} -O3 -march=native -fast -ansi-alias \
    -no-prec-div -qopt-prefetch -unroll-aggressive -auto-ilp32 \
    -fopenmp -finline -funroll-loops -m64 -fma -mkl")

target_include_directories(${PROJECT_NAME} PRIVATE ${PROJECT_SOURCE_DIR}/src)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
