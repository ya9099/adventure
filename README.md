from flask import Flask, render_template, request, redirect, url_for, session

app = Flask(__name__)
app.secret_key = 'your-secret-key'

PERFUMES = {
    'LV': {
        'image': ""C:/Users/omen/Downloads/LV.jpg",
        'ingredients_image': "C:/Users/omen/Downloads/LVingredients.jpg",
        'about_image': ""C:/Users/omen/Downloads/aboutLV.jpg",
        'ratings_image': ""C:/Users/omen/Downloads/LVratings.jpg"
    },
    'GUCCI': {
        'image':"C:/Users/omen/Downloads/GUCCI.jpg",
        'ingredients_image':""C:/Users/omen/Downloads/gucciingredients.jpg",
        'about_image':"C:/Users/omen/Downloads/aboutgucci.jpg",
        'ratings_image': ""C:/Users/omen/Downloads/ratingsgucci.jpg"
    },
    'CHANEL': {
        'image':"C:/Users/omen/Downloads/CHANEL.jpg",
        'ingredients_image':"C:/Users/omen/Downloads/channelingredients.jpg",
        'about_image':""C:/Users/omen/Downloads/aboutchanel.jpg",
        'ratings_image': ""C:/Users/omen/Downloads/ratings.jpg"
    },
    'BELLAVITA': {
        'image':"C:/Users/omen/Downloads/BELAVITTA.jpg",
        'ingredients_image':"C:/Users/omen/Downloads/belavittaingredients.jpg",
        'about_image':"C:/Users/omen/Downloads/aboutbelavitta.jpg",
        'ratings_image':"C:/Users/omen/Downloads/ratingsbellavitta.jpg"
    },
    'RENEE': {
        'image':"C:/Users/omen/Downloads/RENEE.jpg",
        'ingredients_image':"C:/Users/omen/Downloads/reneeingredients.jpg",
        'about_image':"C:/Users/omen/Downloads/aboutrenee.jpg",
        'ratings_image':"C:/Users/omen/Downloads/ratingsrenee.jpg"
    },
    'PARK AVENUE': {
        'image':"C:/Users/omen/Downloads/PARK AVNUE.jpg",
        'ingredients_image':"C:/Users/omen/Downloads/parki.jpg"
        'about_image':"C:/Users/omen/Downloads/aboutparka.jpg" ,
        'ratings_image': "C:/Users/omen/Downloads/ratingsparka.jpg"
    }
}

@app.route('/')
def home():
    return render_template('index.html')

@app.route('/select_perfume')
def select_perfume():
    return render_template('select_perfume.html', perfumes=PERFUMES.keys())

@app.route('/perfume_details/<perfume>')
def perfume_details(perfume):
    session['selected_perfume'] = perfume
    return render_template('perfume_details.html', 
                         perfume=perfume, 
                         perfume_data=PERFUMES[perfume])

@app.route('/view/<category>')
def view_category(category):
    perfume = session.get('selected_perfume')
    if not perfume or perfume not in PERFUMES:
        return redirect(url_for('select_perfume'))
    
    image_key = f'{category}_image'
    return render_template('view_category.html',
                         category=category,
                         image=PERFUMES[perfume][image_key],
                         perfume=perfume)

if __name__ == '__main__':
    app.run(debug=True)
