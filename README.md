# RADAR
Rapid Ad Detection And Removal

A browser bookmarklet that automatically detects and skips sponsored segments in YouTube videos using local LLM inference. This tool analyzes video transcripts to identify and mark sponsored content, providing an enhanced viewing experience.

**Features**

🎯 Automatic sponsor segment detection using local LLM

⏭️ Optional automatic ad skipping

📊 Visual progress bar markers showing ad locations

🎨 Interactive UI for managing detected segments

🎯 Confidence indicators for detected segments

📝 Detailed reasoning for each detected segment

⚡ Real-time transcript analysis

🔧 Configurable detection parameters

**Prerequisites**

A local LLM server running (e.g., LM Studio) on port 1234
YouTube videos must have captions/transcripts available
Modern web browser (Chrome, Firefox, Edge)

**Installation**

Create a new bookmark in your browser
Name it something like "YouTube Ad Detector"
Copy the entire script from bookmarklet
edit the configuration in the bookmarklet and paste the entire code into a bookmarklet maker (i.e https://caiorss.github.io/bookmarklet-maker/)
Drag the bookmarklet to your brower favorites.

**Usage**

Start your local LLM server (default configuration expects it on http://localhost:1234)
Navigate to any YouTube video
Click the bookmark to activate the detector
watch the video and Wait for the analysis to complete

**The tool will:**

Analyze the video transcript
Mark detected sponsor segments on the progress bar (green = normal content, red = sponsored)
Display a control panel showing all detected segments

**Control Panel Features**

Auto-skip Toggle: Automatically skip detected sponsor segments
Progress Bar Markers: Toggle visibility of the visual markers
Segment List: Click any segment to skip to the end of that sponsor section
Confidence Indicators:

🟢 High confidence (≥95%)

🟡 Medium confidence (≥90%)

🟠 Lower confidence (≥85%)



**Configuration**
The script includes a configuration section at the top for customizing:
const CONFIG = {
    llm: {
        base_url: 'http://localhost:1234',
        model: 'llama-3.1-unhinged-vision-8b',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer lm-studio'
        }
    },
    detection: {
        timestampOffset: -3,
        minAdDuration: 15,
        minConfidence: 0.85,
        maxMergeGap: 180,
        autoSkipEnabled: true
    }
};


**LLM Configuration**

base_url: URL of your local LLM server

model: Model name to use for inference

headers: Authentication and content type headers

Detection Configuration

timestampOffset: Adjustment for transcript timing (seconds)

minAdDuration: Minimum duration for ad segments (seconds)

minConfidence: Minimum confidence threshold (0-1)

maxMergeGap: Maximum gap between segments to merge (seconds)

autoSkipEnabled: Enable auto-skip by default

**How It Works**

Transcript Retrieval: Fetches the video's transcript using YouTube's caption system

Initial Filtering: Identifies potentially sponsored segments using keyword matching

LLM Analysis: Processes suspicious segments through a local LLM for detailed analysis

Post-processing: Merges nearby segments and filters based on confidence/duration

Visualization: Displays results and provides interactive controls

**Limitations**

Requires video to have transcripts available

Depends on local LLM server being available

May miss sponsored segments that aren't mentioned in the transcript

Effectiveness may depend on LLM model quality, prompt tuning, and gpu

**Troubleshooting**

Common issues and solutions:

"No captions available": Video must have captions enabled

LLM connection error: Ensure local LLM server is running and accessible

Incorrect segment timing: Adjust timestampOffset in configuration

False positives: Increase minConfidence threshold

Missed segments: Decrease minConfidence threshold or adjust keywords

**Contributing**

Feel free to submit issues and enhancement requests! Areas for improvement:

Additional LLM model support

Improved detection accuracy

UI/UX enhancements

Performance optimizations

Additional configuration options

License
MIT License - feel free to modify and distribute as needed.
Acknowledgments

Uses YouTube's caption system for transcript retrieval
