Project 2 — AI Feedback Intelligence Engine

Overview

The AI Feedback Intelligence Engine is an n8n automation system designed to process customer feedback for a fictional multi-location car-care business.

The project demonstrates how workflow automation, Google Sheets, Gmail, conditional routing, and Google Gemini can be combined to collect feedback, analyse sentiment, identify repeat negative feedback, route cases, and prepare responses for human review.

Business Problem

Customer feedback can require repetitive manual work: identifying completed jobs, requesting feedback, reviewing customer comments, checking previous complaints, deciding how to route issues, and preparing appropriate responses.

This workflow automates these steps while keeping customer-facing responses subject to human review.

Workflow Architecture

The project uses two related workflows:

Workflow A — Feedback Intelligence Engine

This workflow detects completed jobs and sends a customer feedback request.

Flow:

Google Sheets Trigger → IF Status = Complete → Gmail Feedback Request

The feedback request includes the Job ID so the customer's response can be linked back to the original job.

Workflow B — Feedback Reply Handler

This workflow processes submitted feedback.

Main flow:

Google Sheets Trigger → Limit → Loop Over Items → Wait → Google Gemini → Edit Fields → Jobs Lookup → Feedback Log → Repeat Check → Merge → Switch → Routing

The workflow then routes feedback according to its result.

AI Feedback Analysis

Google Gemini is used to analyse the customer's feedback and return:

Sentiment score from -100 to 100

Severity: low, medium, or high

Category: positive or negative

The workflow then uses these values for routing decisions.

Repeat Negative Feedback Detection

The workflow checks the Feedback Log using the customer's email address and negative-feedback category.

This allows the system to identify repeat negative feedback and escalate it when appropriate.

Routing Logic

Positive feedback

Positive feedback is routed to a Ready to Post queue.

Negative feedback

Negative feedback is assessed for severity and repeat history.

Repeat negative feedback or high-severity feedback → Manager Alert

Other negative feedback → Private Queue / Pending Review

Fallback

Feedback that does not match the expected routing conditions is sent to Needs Human Review.

AI-Drafted Response

For negative feedback, Google Gemini can generate an empathetic draft response based on the customer's actual feedback, name, and severity.

The draft is stored in the Feedback Log for review.

Important: The workflow does not automatically publish or send the customer response. Human review is required.

Technologies Used

n8n

Google Sheets

Google Gemini

Gmail

Conditional logic / IF and Switch nodes

Workflow automation

Data Structure

The Feedback Log contains fields including:

Feedback ID

Job ID

Customer Name

Customer Email

Location

Feedback Text

Sentiment Score

Severity

Category

Repeat Negative

Routing Outcome

Draft Response

Alert Status

Testing

The workflow was successfully executed in n8n.

The latest recorded execution completed successfully in approximately 14.857 seconds.

Human-in-the-Loop Design

The project intentionally keeps important customer communication under human oversight. AI is used for analysis and drafting, while routing and response handling provide a review stage before customer-facing action.

Project Evidence

The repository includes a screenshot of the successfully executed n8n workflow:

feedback-intelligence-workflow.png

Project Status

Completed and successfully tested in n8n.
