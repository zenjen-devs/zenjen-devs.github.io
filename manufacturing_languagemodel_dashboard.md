[Back](https://zenjen-devs.github.io)

# Visual Analytics Meets Language Models: Interactive AI for Industrial Intelligence

<img src="images/llm_manufacturing_banner.jpeg?raw=true" title="Source: Adobe Images"/>


[View Repository](https://github.com/zenjen-dev/ml-projects) <br>


*Note: This portfolio section is currently in progress. Please see the project repository linked above for current status.*

<h3> Project Summary </h3>

The convergence of language models and industrial analytics is redefining how we interact with data. Traditional dashboards served their purpose, but we’re now moving into a phase where conversational interfaces, powered by LLMs (Large Language Models), can deliver both insight and interactivity. In this project, I demonstrate how integrating an LLM with visual analytics tools—such as Power BI or Plotly Dash—can augment supply chain decision-making and streamline exploratory analysis.

<h3> Context: From Static Dashboards to Interactive Intelligence</h3>

In modern industrial environments, stakeholders often encounter complex, high-volume datasets/ Dashboards offer static slices, but asking follow-up questions often requires more technical depth or assistance. Language models now allow non-technical users to explore data via natural language without leaving the analytics environment—as demonstrated in the below preview:
<br>

<section class="video-section">
  <div style="max-width: 100%; height: auto;">
    <video style="width: 100%; height: auto;" controls>
      <source src="images/llm_dash.mp4" type="video/mp4">
      Your browser does not support the video tag.
    </video>
  </div>
</section>

Data Source: [Kaggle](https://www.kaggle.com/datasets?tags=12026-Manufacturing/)

### The System: How LLMs Integrate with Visual Analytics

We implemented a basic architecture using OpenAI’s GPT API with a Dash/Streamlit front-end. The goal: Allow users to upload a CSV or query a database, then interact with the results visually and conversationally.

```python
# Callback for chat input
@app.callback(
    Output('chat-response', 'children'),
    Input('submit-chat', 'n_clicks'),
    State('chat-input', 'value')
)
def generate_response(n_clicks, user_input):
    if n_clicks == 0 or not user_input:
        return ""
# ...Query handling specifications, GPT message debug, etc...
    return

# Run the chat app
if __name__ == '__main__':
    app.run(debug=True)
```

The model parses user input, determines the intent (e.g., “Show monthly trend for delayed shipments in Asia-Pacific”), and returns a brief narrative explanation summarizing trends, anomalies, or comparisons.

<br>

### Industrial Use Case Scenario: Supplier Analytics & Risk Forecasting

Real-time supplier analytics are invaluable in an increasingly volatile market. AI-powered dashboards can provide insights instantly with clarity and without technical blocks. 

![Screenshot 2025-04-23 at 6 18 07 PM](https://github.com/user-attachments/assets/30c574de-8070-4ed9-a6d1-f0de6e2867bb)

The project also expands to advanced predictive analytics; In a case where a manufacturer wants to assess supplier delivery risk across multiple locations and overlay that risk with maintenance bulletin timelines. A user asks: “Which suppliers are linked to parts with overdue service bulletins?”

The model:
	- 1.	Filters the dataset to service bulletins marked “Open” and past the effective date.
	- 2.	Cross-references supplier names tied to those part numbers.
	- 3.	Renders a Gantt-style timeline alongside a sortable table of risk rankings.

This kind of interactive querying drastically reduces the time it takes for an engineer or program manager to surface critical information.

### Design Considerations and Challenges

- Data privacy: All prompts and outputs are contained within a secure local environment.
- Explainability: LLMs provide both visual and textual responses for transparency.
- Error handling: Prompts are validated, and fallback responses guide users when queries are ambiguous.
<br>

### How This Project Contributes to Industrial Intelligence

In complex domains—like aerospace, energy, or manufacturing—decision-makers must navigate fragmented data across systems. By embedding natural language interfaces into analytics platforms, we:
	•	Enable faster and deeper exploration.
	•	Make analysis more accessible to non-technical users.
	•	Reduce dependency on data teams for ad hoc insights.

LLM-based analytics are not a replacement for dashboards—they’re an extension of what dashboards could be in a more intelligent, more interactive future.

**References:** [View Repository](https://github.com/zenjen-dev/ml-projects) <br>
