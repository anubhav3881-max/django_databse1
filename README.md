# django_databse1
Jis Id Se logged In Ho Usi Ka Data Show ho uske liye yh likhna hai


✅ अब इसका सही समाधान
1️⃣ जब registration form से data save करें, तो userid भी set करें:
@login_required
def register(request):
    if request.method == 'POST':
        name = request.POST['name']
        email = request.POST['email']
        contact = request.POST['contact']
        city = request.POST['city']
        image = request.FILES.get('image')

        Registration.objects.create(
            name=name,
            email=email,
            contact=contact,
            city=city,
            image=image,
            userid=request.user   # ✅ यह जरूरी है!
        )
        return redirect('displaypage')

    return render(request, 'register.html')

2️⃣ Display page — वही user का data दिखाएगा:
@login_required
def displaypage(request):
    record = Registration.objects.filter(userid=request.user)
    return render(request, 'display.html', {'data': record})
