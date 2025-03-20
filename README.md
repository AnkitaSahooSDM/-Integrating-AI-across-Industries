# -Integrating-AI-across-Industries
## Table of Contents for the Blog Post: "Integrating AI across Industries: Transformations in Healthcare, Marketing, and Finance"
import requests
import nltk
from nltk.corpus import stopwords
from pyseo import SEOAnalyzer
from bs4 import BeautifulSoup

nltk.download('stopwords')

class BlogPostGenerator:
    def __init__(self, industry, topic, key_points, keywords, writing_style):
        self.industry = industry
        self.topic = topic
        self.key_points = key_points
        self.keywords = keywords
        self.writing_style = writing_style
        self.table_of_contents = []
        self.research_data = {}
        self.first_draft = ""
        self.final_draft = ""

    def create_table_of_contents(self):
        self.table_of_contents = [
            "Introduction",
            "Main Body",
            "Conclusion"
        ]
        for key_point in self.key_points:
            self.table_of_contents.append(key_point)

    def research(self):
        # A placeholder research method (could be expanded with web scraping, API integration)
        search_query = f"site:medium.com {self.topic}"
        search_results = requests.get(f"https://www.google.com/search?q={search_query}")
        soup = BeautifulSoup(search_results.text, 'html.parser')
        paragraphs = soup.find_all('p')

        # Extract research data from the webpage content
        for i, para in enumerate(paragraphs[:5]):  # Just an example: first 5 paragraphs
            self.research_data[f"Research Point {i+1}"] = para.get_text()

    def generate_first_draft(self):
        self.first_draft += f"# {self.topic}\n\n"
        self.first_draft += "## Introduction\n"
        self.first_draft += f"Introduction about {self.topic} in the context of {self.industry}.\n\n"
        
        # Populate body with key points and research data
        for key_point in self.key_points:
            self.first_draft += f"## {key_point}\n"
            self.first_draft += f"Details about {key_point} with supporting research.\n"
            self.first_draft += f"Research: {self.research_data.get(f'Research Point {self.key_points.index(key_point)+1}', 'No data')}\n\n"
        
        self.first_draft += "## Conclusion\n"
        self.first_draft += "Summarizing the main insights and final thoughts.\n"

    def apply_feedback(self, feedback):
        # Simple feedback method for applying edits (could be expanded for detailed changes)
        self.final_draft = self.first_draft + "\n" + feedback

    def optimize_for_seo(self):
        seo_analyzer = SEOAnalyzer(self.final_draft)
        seo_score = seo_analyzer.analyze()
        
        # Improve content for SEO if necessary
        if seo_score < 80:
            print("Optimizing content for SEO...")
            # Example: replace keywords or adjust density
            for keyword in self.keywords:
                if keyword not in self.final_draft:
                    self.final_draft += f"\n\nAdditional info about {keyword}."
        else:
            print("SEO optimization not needed.")

    def generate_title(self):
        title = f"Comprehensive Guide on {self.topic} for {self.industry}"
        return title

    def generate_blog_post(self, feedback=""):
        self.create_table_of_contents()
        self.research()
        self.generate_first_draft()
        self.apply_feedback(feedback)
        self.optimize_for_seo()
        title = self.generate_title()

        return title, self.final_draft


# Example Usage
industry = "Technology"
topic = "Artificial Intelligence in Healthcare"
key_points = ["AI Applications", "Challenges", "Future of AI"]
keywords = ["AI", "machine learning", "healthcare"]
writing_style = "Conversational"

blog_post_generator = BlogPostGenerator(industry, topic, key_points, keywords, writing_style)
title, blog_post = blog_post_generator.generate_blog_post(feedback="Improve clarity in conclusion.")

print(f"Title: {title}")
print("\nBlog Post:\n")
print(blog_post)
