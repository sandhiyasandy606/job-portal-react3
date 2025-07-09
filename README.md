// Language & Tech Stack Used:
// - Language: JavaScript (React.js framework)
// - UI Library: ShadCN/UI (based on Tailwind CSS)
// - Styling: Tailwind CSS
// - State Management: React useState
// - Components: Input, Button, Card, Dialog

import React, { useState, useEffect } from "react";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { Dialog, DialogContent, DialogTrigger } from "@/components/ui/dialog";

const mockJobs = [
  { id: 1, title: "Frontend Developer", location: "Chennai", skills: "React, CSS", resume: "Uploaded" },
  { id: 2, title: "Backend Developer", location: "Bangalore", skills: "Node.js, MongoDB", resume: "Uploaded" },
];

export default function JobPortal() {
  const [jobs, setJobs] = useState(mockJobs);
  const [search, setSearch] = useState("");
  const [title, setTitle] = useState("");
  const [location, setLocation] = useState("");
  const [skills, setSkills] = useState("");

  const handlePostJob = () => {
    const newJob = {
      id: jobs.length + 1,
      title,
      location,
      skills,
      resume: "Uploaded"
    };
    setJobs([...jobs, newJob]);
    setTitle("");
    setLocation("");
    setSkills("");
  };

  const filteredJobs = jobs.filter(job =>
    job.title.toLowerCase().includes(search.toLowerCase()) ||
    job.location.toLowerCase().includes(search.toLowerCase()) ||
    job.skills.toLowerCase().includes(search.toLowerCase())
  );

  return (
    <div className="p-4 max-w-4xl mx-auto">
      <h1 className="text-2xl font-bold mb-4">Job Portal</h1>

      <Input
        placeholder="Search job title, location or skills..."
        value={search}
        onChange={(e) => setSearch(e.target.value)}
        className="mb-4"
      />

      <Dialog>
        <DialogTrigger asChild>
          <Button className="mb-4">Post a Job</Button>
        </DialogTrigger>
        <DialogContent>
          <h2 className="text-xl font-bold mb-2">Post a New Job</h2>
          <Input
            placeholder="Job Title"
            value={title}
            onChange={(e) => setTitle(e.target.value)}
            className="mb-2"
          />
          <Input
            placeholder="Location"
            value={location}
            onChange={(e) => setLocation(e.target.value)}
            className="mb-2"
          />
          <Input
            placeholder="Required Skills"
            value={skills}
            onChange={(e) => setSkills(e.target.value)}
            className="mb-4"
          />
          <Button onClick={handlePostJob}>Submit</Button>
        </DialogContent>
      </Dialog>

      <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
        {filteredJobs.map((job) => (
          <Card key={job.id} className="shadow">
            <CardContent className="p-4">
              <h3 className="text-lg font-semibold">{job.title}</h3>
              <p className="text-sm text-gray-600">{job.location}</p>
              <p className="text-sm">Skills: {job.skills}</p>
              <p className="text-sm text-green-600">Resume: {job.resume}</p>
            </CardContent>
          </Card>
        ))}
      </div>
    </div>
  );
}
