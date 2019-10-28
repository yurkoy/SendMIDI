cmake_minimum_required(VERSION 3.4)

project(SendMIDI)

find_package (Threads REQUIRED)
find_package (ALSA REQUIRED)
find_package (CURL REQUIRED)


add_executable(sendmidi
	"Source/Main.cpp"
	"JuceLibraryCode/include_juce_audio_basics.cpp"
	"JuceLibraryCode/include_juce_audio_devices.cpp"
	"JuceLibraryCode/include_juce_core.cpp"
	"JuceLibraryCode/include_juce_data_structures.cpp"
	"JuceLibraryCode/include_juce_events.cpp"
)

target_compile_definitions(sendmidi PRIVATE
	"LINUX=1"
	"DEBUG=1"
	"_DEBUG=1"
	"JUCE_LINUX_MAKE_6D53C8B4=1"
	"JUCE_APP_VERSION=1.0.15"
	"JUCE_APP_VERSION_HEX=0x1000f"
	"JucePlugin_Build_VST=0"
	"JucePlugin_Build_VST3=0"
	"JucePlugin_Build_AU=0"
	"JucePlugin_Build_AUv3=0"
	"JucePlugin_Build_RTAS=0"
	"JucePlugin_Build_AAX=0"
	"JucePlugin_Build_Standalone=0"
	"JucePlugin_Build_Unity=0"
)

target_compile_options(sendmidi PRIVATE
	"-ggdb"
)

target_include_directories(sendmidi PRIVATE
	${ALSA_INCLUDE_DIRS}
	${CURL_INCLUDE_DIRS}
	"JuceLibraryCode"
	"JuceLibraryCode/modules"
)

target_link_libraries(sendmidi
	${CMAKE_DL_LIBS}
	Threads::Threads
	${ALSA_LIBRARIES}
	${CURL_LIBRARIES}
)

set_target_properties(sendmidi PROPERTIES
	CXX_STANDARD 14
)

install(TARGETS sendmidi DESTINATION ".")
