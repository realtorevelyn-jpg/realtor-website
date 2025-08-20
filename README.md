import React, { useMemo, useState } from "react";
import { motion } from "framer-motion";
import { Button } from "@/components/ui/button";
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Textarea } from "@/components/ui/textarea";
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select";
import { Dialog, DialogContent, DialogHeader, DialogTitle, DialogDescription, DialogTrigger } from "@/components/ui/dialog";
import { Badge } from "@/components/ui/badge";
import { CheckCircle, Phone, Mail, MapPin, Download, FileText, Calendar, ShieldCheck, Sparkles, Star } from "lucide-react";


// =========================================
// Evelyn Malave — Lead Magnet Website
// =========================================


// -------- Guide URLs (replace with your actual uploaded PDFs) --------
function useGuideDownloadUrls() {
return [
{
key: "buyer",
filename: "Home-Buyer-Guide-Evelyn-Malave.pdf",
title: "Free Home Buyer Guide",
url: "https://yourdomain.com/pdfs/Home-Buyer-Guide.pdf", // TODO: replace with real URL
},
{
key: "relocation",
filename: "Relocation-to-Florida-Guide-Evelyn-Malave.pdf",
title: "Relocation to Florida Guide",
url: "https://yourdomain.com/pdfs/Relocation-Guide.pdf", // TODO: replace with real URL
},
{
key: "seller",
filename: "Home-Seller-Guide-Evelyn-Malave.pdf",
title: "Home Seller Guide",
url: "https://yourdomain.com/pdfs/Seller-Guide.pdf", // TODO: replace with real URL
},
];
}


// -------- Types --------
interface LeadFormData {
fullName: string;
email: string;
phone: string;
timeline: string;
message: string;
guideChoice: "buyer" | "relocation" | "seller" | "all";
consent: boolean;
}


const DEFAULT_FORM: LeadFormData = {
fullName: "",
email: "",
phone: "",
timeline: "",
message: "",
guideChoice: "buyer",
consent: false,
};


export default function RealEstateLeadMagnetSite() {
const [form, setForm] = useState<LeadFormData>({ ...DEFAULT_FORM });
const [submitted, setSubmitted] = useState(false);
const [submitting, setSubmitting] = useState(false);
const [error, setError] = useState<string | null>(null);


const guideUrls = useGuideDownloadUrls();


const update = (patch: Partial<LeadFormData>) => setForm(prev => ({ ...prev, ...patch }));


const validate = () => {
if (!form.fullName.trim()) return "Please enter your full name.";
if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) return "Please enter a valid email address.";
if (!/^[0-9+()\-\s]{7,}$/.test(form.phone)) return "Please enter a valid phone number.";
if (!form.timeline) return "Please select your timeframe.";
if (!form.consent) return "Please agree to be contacted.";
return null;
};


const handleSubmit = async (e?: React.FormEvent) => {
e?.preventDefault();
setError(null);
// (Keep all the subcomponents: FeaturePill, Bullet, StatCard, GuideCard, LeadForm — unchanged from earlier version)
