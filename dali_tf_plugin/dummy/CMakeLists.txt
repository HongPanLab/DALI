# Copyright (c) 2020, NVIDIA CORPORATION. All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

cmake_minimum_required(VERSION 3.2)
project(dali_tf_dummy)

set(DALI_ROOT "${PROJECT_SOURCE_DIR}/../..")

SET(CUDA_VERSION "" CACHE STRING "CUDA version")
if ("${CUDA_VERSION}" STREQUAL "")
  message(FATAL_ERROR "CUDA version not provided. Pass CUDA version to cmake (e.g -DCUDA_VERSION:STRING=\"10.1\")")
endif()

include(${DALI_ROOT}/cmake/Utils.cmake)
parse_cuda_version(${CUDA_VERSION} CUDA_VERSION_MAJOR CUDA_VERSION_MINOR CUDA_VERSION_PATCH CUDA_VERSION_SHORT CUDA_VERSION_SHORT_DIGIT_ONLY)

get_dali_version(${DALI_ROOT}/VERSION DALI_VERSION)
if (DALI_BUILD_FLAVOR)
  set(DALI_FLAVOR "${DALI_BUILD_FLAVOR} ")
  set(DALI_FLAVOR_MINUS "-${DALI_BUILD_FLAVOR}")
  set(DALI_VERSION "${DALI_VERSION}.${TIMESTAMP}")
endif()

configure_file("${PROJECT_SOURCE_DIR}/setup.py.in" "${PROJECT_BINARY_DIR}/setup.py")
