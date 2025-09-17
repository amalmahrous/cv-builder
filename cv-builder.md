import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Textarea } from "@/components/ui/textarea";
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select";

export default function CVBuilder() {
  const [lang, setLang] = useState("ar");
  const [data, setData] = useState({
    name: "",
    email: "",
    phone: "",
    address: "",
    summary: "",
    experience: "",
    education: "",
    skills: "",
    languages: "",
  });
  const [photo, setPhoto] = useState(null);

  const labels = {
    ar: {
      personal: "البيانات الشخصية",
      name: "الاسم الكامل",
      email: "البريد الإلكتروني",
      phone: "رقم الهاتف",
      address: "العنوان",
      summary: "الملخص المهني",
      experience: "الخبرات العملية",
      education: "التعليم",
      skills: "المهارات",
      languages: "اللغات",
      upload: "رفع صورة شخصية",
      template: "اختيار التصميم",
      download: "تحميل السيرة الذاتية",
      switch: "English",
    },
    en: {
      personal: "Personal Information",
      name: "Full Name",
      email: "Email",
      phone: "Phone Number",
      address: "Address",
      summary: "Professional Summary",
      experience: "Work Experience",
      education: "Education",
      skills: "Skills",
      languages: "Languages",
      upload: "Upload Profile Photo",
      template: "Choose Template",
      download: "Download CV",
      switch: "عربي",
    },
  };

  const t = labels[lang];

  return (
    <div className="min-h-screen p-6 bg-gray-100">
      {/* Header */}
      <div className="flex justify-between items-center mb-6">
        <h1 className="text-2xl font-bold">{lang === "ar" ? "منشئ السيرة الذاتية" : "CV Builder"}</h1>
        <Button onClick={() => setLang(lang === "ar" ? "en" : "ar")}>
          {t.switch}
        </Button>
      </div>

      {/* Form */}
      <div className="grid md:grid-cols-2 gap-6">
        <Card>
          <CardContent className="space-y-4 p-4">
            <h2 className="font-semibold text-lg">{t.personal}</h2>
            <Input placeholder={t.name} onChange={(e) => setData({ ...data, name: e.target.value })} />
            <Input placeholder={t.email} onChange={(e) => setData({ ...data, email: e.target.value })} />
            <Input placeholder={t.phone} onChange={(e) => setData({ ...data, phone: e.target.value })} />
            <Input placeholder={t.address} onChange={(e) => setData({ ...data, address: e.target.value })} />
            <div>
              <label className="block mb-2">{t.upload}</label>
              <Input type="file" accept="image/*" onChange={(e) => setPhoto(URL.createObjectURL(e.target.files[0]))} />
            </div>

            <Textarea placeholder={t.summary} onChange={(e) => setData({ ...data, summary: e.target.value })} />
            <Textarea placeholder={t.experience} onChange={(e) => setData({ ...data, experience: e.target.value })} />
            <Textarea placeholder={t.education} onChange={(e) => setData({ ...data, education: e.target.value })} />
            <Textarea placeholder={t.skills} onChange={(e) => setData({ ...data, skills: e.target.value })} />
            <Textarea placeholder={t.languages} onChange={(e) => setData({ ...data, languages: e.target.value })} />

            <div>
              <label className="block mb-2">{t.template}</label>
              <Select>
                <SelectTrigger>
                  <SelectValue placeholder="Default" />
                </SelectTrigger>
                <SelectContent>
                  <SelectItem value="classic">Classic</SelectItem>
                  <SelectItem value="modern">Modern</SelectItem>
                  <SelectItem value="creative">Creative</SelectItem>
                </SelectContent>
              </Select>
            </div>

            <Button className="w-full mt-4">{t.download}</Button>
          </CardContent>
        </Card>

        {/* CV Preview */}
        <Card>
          <CardContent className="p-4">
            <div className="flex gap-4 items-center">
              {photo && <img src={photo} alt="Profile" className="w-24 h-24 rounded-full object-cover" />}
              <div>
                <h2 className="text-xl font-bold">{data.name}</h2>
                <p>{data.email}</p>
                <p>{data.phone}</p>
                <p>{data.address}</p>
              </div>
            </div>

            <div className="mt-4">
              <h3 className="font-semibold">{t.summary}</h3>
              <p>{data.summary}</p>
            </div>

            <div className="mt-4">
              <h3 className="font-semibold">{t.experience}</h3>
              <p>{data.experience}</p>
            </div>

            <div className="mt-4">
              <h3 className="font-semibold">{t.education}</h3>
              <p>{data.education}</p>
            </div>

            <div className="mt-4">
              <h3 className="font-semibold">{t.skills}</h3>
              <p>{data.skills}</p>
            </div>

            <div className="mt-4">
              <h3 className="font-semibold">{t.languages}</h3>
              <p>{data.languages}</p>
            </div>
          </CardContent>
        </Card>
      </div>
    </div>
  );
}
