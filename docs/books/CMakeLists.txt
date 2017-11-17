##
## Licensed to the Apache Software Foundation (ASF) under one
## or more contributor license agreements.  See the NOTICE file
## distributed with this work for additional information
## regarding copyright ownership.  The ASF licenses this file
## to you under the Apache License, Version 2.0 (the
## "License"); you may not use this file except in compliance
## with the License.  You may obtain a copy of the License at
##
##   http://www.apache.org/licenses/LICENSE-2.0
##
## Unless required by applicable law or agreed to in writing,
## software distributed under the License is distributed on an
## "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
## KIND, either express or implied.  See the License for the
## specific language governing permissions and limitations
## under the License.
##

find_program (ASCIIDOCTOR_EXE asciidoctor DOC "Generate books")

set (
  BOOKS
  "${CMAKE_CURRENT_BINARY_DIR}/user-guide/index.html"
  )

if (ASCIIDOCTOR_EXE)
  add_custom_command (
    OUTPUT ${BOOKS}
    COMMAND ${ASCIIDOCTOR_EXE} ${CMAKE_CURRENT_SOURCE_DIR}/user-guide/book.adoc -o user-guide/index.html
    DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/user-guide/book.adoc
    )
else ()
  message (STATUS "AsciiDoctor not found: Not generating books")
endif ()

add_custom_target(books DEPENDS ${BOOKS})
add_dependencies(doc books)
