GEMINI_API_KEY=AIzaSyDPLmnAkBuk7I5i_YS7jnY4KfZzcXtEGpg

import { GoogleGenerativeAI } from "@google/generative-ai";
import { readFile, writeFile } from "fs/promises";
import { resolve } from "path";
import fetch, { Headers, Request, Response } from "node-fetch";
import dotenv from "dotenv";
dotenv.config();
 
Object.assign(globalThis, { fetch, Headers, Request, Response });
const genAI = new GoogleGenerativeAI(process.env.GEMINI_API_KEY);
const model = genAI.getGenerativeModel({ model: "gemini-2.5-pro" });
 
const file = resolve("App.test.js");
const prompt = await readFile(file, "utf-8");
const res = await model.generateContent(prompt);
const text = res.response.text();
 
console.log(text);
await writeFile(resolve("output.txt"), text);
console.log("Output written to output.txt");
//npm init -y
//npm i dotenv @google/generative-ai node-fetch@3
//Node App.mjs
