## --აგი პითონის ფაილები აგენერირებენ ვორდლისტებს--
## ❌თავად ვორდლისტები არ არის ამ რეპოში აქ არის პითონის ფაილი რომელიც მათ აგენერირებს❌
## ❌ გაფრთხილება ❌
 სუსტ კომპებს უჭირთ NS_Generator_Mixer.py-ს და All_Geo_numbers.py-ს გაშვება
 
## პითნის ფაილების შესახებ

"თავად ფაილებშიც ბლომად კომენტარებია იმედია დაგეხმარება"

 NS_Generator_Mixer(NameSurname_Generator_Mixer)-ით გენერირდება 35000000+ (2̶0̶0̶0̶0̶0̶0̶+̶)  - ქართული სახელების და გვარების სხვადასხვა განლაგებით wordlst-ი
 
 ALL_Geo_numbers-ით გენერირდება ყველა ქართული ტელეფონის ნომერი

 New_pas_Creator_Terninal და New_pas_Creator_No_Terninal - შეყვანილი სიტყვით აკეთებს wordlist-ს. (ბევრი კომენტარი აქვს იმედია უფრო არ
 დაგაბნევს)

 years - აგენერირებს წლებს 1920 - 2025 ამდე და ასევე ამატებს დღისა და თვის აღმნიშვნელ რიცხვებს თავში და ბოლოში

## მოდიფიცირების საშუალება

Names და Surnames დირექტორიებში არსებულ ფაილებში შეიძლება კიდევ სხვა სახელების და გვარების დამატება.
რეალურად არ არის აუცილებელი რომ დამატებული სიტყვები იყოს სახელი ან გვარი.

მარტივია კოდის მოდიფიცირება ისე რომ დაემატოს კიდევ მრავალი კომბინაცია. შევეცადე ბევრი და გასაგები კომენტარი დამერთო ქართულ ენაზე (ვცდილობ მაქსიმალურად ქართულად იყოს)

როგორ შეგიძლია დაამოდიფიცირო წერია ქვემოთ 👇 "დახმარება მოდიფიცირებაში" გრაფაში

## რას აკეთებს კოდი NS_Generator_Mixer

წარმოვიდგინოთ რომ Names-ს ფაილში წერია სიტყვა saxeli ხოლო Surnames-ს ფაილში წერია სიტყვა gvari,
NS_Generator_Mixer-ი გააკეთებს ასეთ რაღაცას:

1) დუპლიკანტების მოშორება - ამოიღებს უნიკალურ სიტყვებს

2) უნიკალურ სიტყვებს დაწერს დიდი და პატარა ასოებით აი ასე: saxeli Saxeli SAXELI. | იგივეს იზამს გვარებზე

3) სახელების და გვარების შერევა, გააკეთებს ასეთ რაღაცას 
* saxeligvari
* saxeliGvari
* saxeliGVARI
* Saxeligvari
* SaxeliGvari
* SaxeliGVARI
* SAXELIgvari
* SAXELIGvari
* SAXELIGVARI

შემდეგ იგივეს იზამს პირიქით ანუ:

* gvarisaxeli
* gvariSaxeli...

ასევე გააკეთებს იგივე პრინციპით დიდი და პატარა ასოებით შერევას და მათ შორის დაწერს სხვადასხვა სიმბოლოს:
* saxeli.gvari
* saxeli_gvari
* saxeli-gvari
* saxeli/gvari
* saxeli\gvari
* s.gvari
* s_gvari
* s-gvari
* s/gvari
* s\gvari

4) შლის 8 ზე ნაკლებ ასოიან სიტყვებს

## დახმარება მოდიფიცირებაში

* დიდი და პატარა ასოების მოდიფიცირება - ხაზი 32

```
    # აქ შეგიძლია დაამატო სხვადასხვა ვარიანტი
    lowercase_lines = [line.lower() for line in lines]
    first_letter_uppercase_lines = [line.capitalize() for line in lines]
    uppercase_lines = [line.upper() for line in lines]
```
რაიმეს დამატების შემდეგ აქ ჩაამატე outfile.writelines(რასაც დაარქმევ ახალ ვარიანტს)
```
with open(output_file, 'w', encoding='utf-8') as outfile:
        outfile.writelines(lowercase_lines)
        outfile.writelines(first_letter_uppercase_lines)
        outfile.writelines(uppercase_lines)
```

* სახელებისა და გვარების შერევა  - ხაზი 105

```
    # აქ შეგიძლია დაამატო კომბინაციები 
    combination1 = [f"{name}{surname}" for name in names for surname in surnames]
    combination2 = [f"{name}_{surname}" for name in names for surname in surnames]
    combination3 = [f"{name}-{surname}" for name in names for surname in surnames]
    combination4 = [f"{name}.{surname}" for name in names for surname in surnames]
    combination5 = [f"{name}/{surname}" for name in names for surname in surnames]
    combination6 = [f"{name}\{surname}" for name in names for surname in surnames]
    combination7 = [f"{name[0]}.{surname}" for name in names for surname in surnames]
    combination8 = [f"{name[0]}_{surname}" for name in names for surname in surnames]
    combination9 = [f"{name[0]}-{surname}" for name in names for surname in surnames]
    combination10 = [f"{name[0]}/{surname}" for name in names for surname in surnames]
    combination11 = [f"{name[0]}\{surname}" for name in names for surname in surnames]
    combination12 = [f"{name[0]}_{surname}" for name in names for surname in surnames]
    combination13 = [f"{name[0]}{surname}" for name in names for surname in surnames]
```

რაიმეს დამატების შემდეგ აქ ჩაამატე outfile.writelines(რასაც დაარქმევ ახალ ვარიანტს)
```
with open(output_file, 'w', encoding='utf-8') as outfile:
        outfile.write("\n".join(combination1) + "\n")
        outfile.write("\n".join(combination2) + "\n")
        outfile.write("\n".join(combination3) + "\n")
        outfile.write("\n".join(combination4) + "\n")
        outfile.write("\n".join(combination5) + "\n")
        outfile.write("\n".join(combination6) + "\n")
        outfile.write("\n".join(combination7) + "\n")
        outfile.write("\n".join(combination8) + "\n")
        outfile.write("\n".join(combination9) + "\n")
        outfile.write("\n".join(combination10) + "\n")
        outfile.write("\n".join(combination11) + "\n")
        outfile.write("\n".join(combination12) + "\n")
        outfile.write("\n".join(combination13) + "\n")
```
(ფორ ციკლი შეილება კი)


* დროებითი ფაილების წაშლა - ხაზი 225

კოდი სამუშაოს დასრულების შემდეგ ქმნის დროებით ფაილებს რომელსაც ავტომატურად შლის,
შეგიძლია მისი დაკომენტარება ან საერთოდ წაშლა თუ გსურს რომ დროებითი ფაილები არ წაიშალოს