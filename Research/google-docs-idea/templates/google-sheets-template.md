# Google Sheets Template for YouTube Shorts Automation

## Sheet Structure

Create a Google Sheet with the following columns:

### Main Projects Sheet

| Column | Description | Type | Example |
|--------|-------------|------|---------|
| ID | Unique identifier | Text | PROJ_001 |
| Idea | User's initial video idea | Text | "Explain quantum physics in simple terms" |
| Status | Current workflow stage | Dropdown | Pending, Concept Review, Script Review, etc. |
| Created | Timestamp of creation | Date | 2024-01-15 10:30 |
| Updated | Last update timestamp | Date | 2024-01-15 14:22 |
| Concept | AI-generated concept | Long Text | JSON concept object |
| ConceptApproved | User approval status | Dropdown | Yes, No, Needs Changes |
| ConceptFeedback | User feedback on concept | Text | "Make it more engaging for teens" |
| Script | AI-generated script/storyboard | Long Text | JSON script object |
| ScriptApproved | User approval status | Dropdown | Yes, No, Needs Changes |
| ScriptFeedback | User feedback on script | Text | "Slow down the pace" |
| VisualsApproved | User approval for visuals | Dropdown | Yes, No, Needs Changes |
| VisualsFeedback | User feedback on visuals | Text | "Use brighter colors" |
| AudioApproved | User approval for audio | Dropdown | Yes, No, Needs Changes |
| AudioFeedback | User feedback on audio | Text | "Use female voice" |
| VideoURL | Generated video URL | URL | https://drive.google.com/... |
| FinalApproved | Final video approval | Dropdown | Yes, No, Needs Changes |
| FinalFeedback | Final feedback | Text | "Perfect!" |
| YouTubeURL | Published YouTube URL | URL | https://youtu.be/... |
| Title | Generated YouTube title | Text | "Quantum Physics Explained in 60 Seconds" |
| Description | Generated description | Long Text | Video description |
| Tags | Generated tags | Text | physics,science,education |

### Status Values (Dropdown Options)

1. **Pending** - Initial state, waiting for concept generation
2. **Concept Review** - Concept generated, waiting for user approval
3. **Concept Revision** - User requested changes to concept
4. **Script Review** - Script generated, waiting for user approval
5. **Script Revision** - User requested changes to script
6. **Visual Generation** - Creating scene images
7. **Visual Review** - Visuals ready for user approval
8. **Visual Revision** - User requested visual changes
9. **Audio Generation** - Creating voiceover
10. **Audio Review** - Audio ready for user approval
11. **Audio Revision** - User requested audio changes
12. **Video Assembly** - Assembling final video
13. **Final Review** - Complete video ready for approval
14. **Final Revision** - User requested final changes
15. **Publishing** - Uploading to YouTube
16. **Published** - Video live on YouTube
17. **Error** - Workflow encountered an error

### Approval Values (Dropdown Options)

- **Yes** - Approved, proceed to next stage
- **No** - Rejected, needs major revision
- **Needs Changes** - Approved with minor changes requested

## Google Sheets Formula Examples

### Auto-update timestamps:
```
=IF(B2<>"",(IF(C2<>E2,NOW(),E2)),"")
```

### Status tracking:
```
=IF(F2="Yes","Script Review",IF(F2="Needs Changes","Concept Revision","Concept Review"))
```

### Progress indicator:
```
=SWITCH(C2,
  "Published", "✅ Complete",
  "Final Review", "🎬 90%",
  "Video Assembly", "🔧 80%",
  "Audio Review", "🎵 70%",
  "Visual Review", "🎨 60%",
  "Script Review", "📝 40%",
  "Concept Review", "💡 20%",
  "Pending", "⏳ 0%",
  "❌ Error"
)
```

## Setup Instructions

1. Create a new Google Sheet
2. Add the columns as specified above
3. Set up data validation for dropdown columns
4. Apply conditional formatting for status visualization
5. Share the sheet with your n8n service account
6. Copy the sheet ID for use in the workflow

## Color Coding (Conditional Formatting)

- **Green**: Approved statuses (Yes)
- **Yellow**: Pending review statuses
- **Red**: Rejected or error statuses
- **Blue**: In-progress statuses

## Usage Workflow

1. User adds new row with ID and Idea
2. Sets Status to "Pending"
3. n8n workflow picks up pending items
4. User receives notifications for each approval stage
5. User updates approval columns with feedback
6. Workflow continues based on approval status
7. Final video gets published automatically when approved