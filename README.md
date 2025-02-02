# Chat-bot-Project
npx create-react-app chatbot-frontend
   cd chatbot-frontend
   pip install fastapi uvicorn sqlalchemy langgraph transformers
from sqlalchemy import create_engine, Column, Integer, String, Float, Text
     from sqlalchemy.ext.declarative import declarative_base

     DATABASE_URL = "postgresql://user:password@localhost/dbname"
     engine = create_engine(DATABASE_URL)
     Base = declarative_base()

     class Product(Base):
         _tablename_ = "products"
         id = Column(Integer, primary_key=True, index=True)
         name = Column(String, index=True)
         brand = Column(String)
         price = Column(Float)
         category = Column(String)
         description = Column(Text)
         supplier_id = Column(Integer)

     class Supplier(Base):
         _tablename_ = "suppliers"
         id = Column(Integer, primary_key=True, index=True)
         name = Column(String)
         contact_info = Column(Text)
         product_categories_offered = Column(Text)
from transformers import pipeline

     summarizer = pipeline("summarization", model="facebook/bart-large-cnn")
     summary = summarizer("Supplier A provides laptops and phones. Contact: contact@supplierA.com.")
     print(summary)
from fastapi import FastAPI, HTTPException
     app = FastAPI()

     @app.post("/query")
     async def handle_query(query: str):
         # Fetch data from database
         # Use LLM to summarize data
         return {"response": "Enhanced response from LLM"}
CREATE TABLE products (
       id SERIAL PRIMARY KEY,
       name VARCHAR(255) NOT NULL,
       brand VARCHAR(255) NOT NULL,
       price DECIMAL(10, 2) NOT NULL,
       category VARCHAR(255) NOT NULL,
       description TEXT,
       supplier_id INT REFERENCES suppliers(id)
   );
CREATE TABLE suppliers (
       id SERIAL PRIMARY KEY,
       name VARCHAR(255) NOT NULL,
       contact_info TEXT NOT NULL,
       product_categories_offered TEXT
   );
INSERT INTO suppliers (name, contact_info, product_categories_offered)
  VALUES ('Supplier A', 'contact@supplierA.com', 'laptops, phones');

  INSERT INTO products (name, brand, price, category, description, supplier_id)
  VALUES ('Laptop X', 'Brand X', 1200.00, 'laptops', 'High-performance laptop', 1);
SELECT * FROM products WHERE brand = 'Brand X';
SELECT * FROM suppliers WHERE product_categories_offered LIKE '%laptops%';
