## --აგი პითონის ფაილები აგენერირებენ ვორდლისტებს--
## ❌თავად ვორდლისტები არ არის ამ რეპოში აქ არის პითონის ფაილი რომელიც მათ აგენერირებს❌

 
## პითნის ფაილების შესახებ
 NS_Generator_Mixer(NameSurname_Generator_Mixer)-ით გენერირდება 2000000+ ქართული სახელების და გვარების სხვადასხვა განლაგებით wordlst-ი
 
 ALL_Geo_numbers-ით გენერირდება ყველა ქართული ტელეფონის ნომერი 

## მოდიფიცირების საშუალება

Names და Surnames დირექტორიებში არსებულ ფაილებში შეიძლება კიდევ სხვა სახელების და გვარების დამატება.
რეალურად არ არის აუცილებელი რომ დამატებული სიტყვები იყოს სახელი ან გვარი.

მარტივია კოდის მოდიფიცირება ისე რომ დაემატოს კიდევ მრავალი კომბინაცია.

როგორ შეგიძლია დაამოდიფიცირო წერია ქვემოთ 👇 "დახმარება მოდიფიცირებაში" გრაფაში

## რას აკეთებს კოდი

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

* დიდი და პატარა ასოების მოდიფიცირება - ხაზი 30

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

* კომბინაციების მოდიფიცირება - ხაზი 62

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