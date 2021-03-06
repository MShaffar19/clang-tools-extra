set(LLVM_LINK_COMPONENTS
  Support
  )

set(CLANGD_ATOMIC_LIB "")
if(NOT HAVE_CXX_ATOMICS64_WITHOUT_LIB)
  list(APPEND CLANGD_ATOMIC_LIB "atomic")
endif()

add_clang_library(clangDaemon
  AST.cpp
  Cancellation.cpp
  ClangdLSPServer.cpp
  ClangdServer.cpp
  ClangdUnit.cpp
  CodeComplete.cpp
  CodeCompletionStrings.cpp
  Compiler.cpp
  Context.cpp
  Diagnostics.cpp
  DraftStore.cpp
  ExpectedTypes.cpp
  FindSymbols.cpp
  FileDistance.cpp
  FS.cpp
  FuzzyMatch.cpp
  GlobalCompilationDatabase.cpp
  Headers.cpp
  JSONTransport.cpp
  Logger.cpp
  Protocol.cpp
  Quality.cpp
  RIFF.cpp
  SourceCode.cpp
  Threading.cpp
  Trace.cpp
  TUScheduler.cpp
  URI.cpp
  XRefs.cpp

  index/Background.cpp
  index/BackgroundIndexStorage.cpp
  index/CanonicalIncludes.cpp
  index/FileIndex.cpp
  index/Index.cpp
  index/IndexAction.cpp
  index/MemIndex.cpp
  index/Merge.cpp
  index/Serialization.cpp
  index/SymbolCollector.cpp
  index/YAMLSerialization.cpp

  index/dex/Dex.cpp
  index/dex/Iterator.cpp
  index/dex/PostingList.cpp
  index/dex/Trigram.cpp

  LINK_LIBS
  clangAST
  clangASTMatchers
  clangBasic
  clangDriver
  clangFormat
  clangFrontend
  clangIndex
  clangLex
  clangSema
  clangSerialization
  clangTidy
  clangTidyAndroidModule
  clangTidyAbseilModule
  clangTidyBoostModule
  clangTidyBugproneModule
  clangTidyCERTModule
  clangTidyCppCoreGuidelinesModule
  clangTidyFuchsiaModule
  clangTidyGoogleModule
  clangTidyHICPPModule
  clangTidyLLVMModule
  clangTidyMiscModule
  clangTidyModernizeModule
  clangTidyObjCModule
  clangTidyPerformanceModule
  clangTidyPortabilityModule
  clangTidyReadabilityModule
  clangTidyZirconModule
  clangTooling
  clangToolingCore
  clangToolingInclusions
  clangToolingRefactor
  ${LLVM_PTHREAD_LIB}
  ${CLANGD_ATOMIC_LIB}
  )

if( LLVM_LIB_FUZZING_ENGINE OR LLVM_USE_SANITIZE_COVERAGE )
  add_subdirectory(fuzzer)
endif()
add_subdirectory(tool)
add_subdirectory(indexer)
add_subdirectory(index/dex/dexp)

if (LLVM_INCLUDE_BENCHMARKS)
  add_subdirectory(benchmarks)
endif()
