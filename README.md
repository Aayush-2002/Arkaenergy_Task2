# Arkaenergy_Task2

# models.py
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)
    age = models.IntegerField()
    email = models.EmailField(unique=True)

    def __str__(self):
        return self.name


# serializers.py
from rest_framework import serializers
from .models import Student

class StudentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Student
        fields = '__all__'

# views.py
from rest_framework import generics
from .models import Student
from .serializers import StudentSerializer

class StudentListCreateAPIView(generics.ListCreateAPIView):
    queryset = Student.objects.all()
    serializer_class = StudentSerializer


# urls.py
from django.urls import path
from .views import StudentListCreateAPIView

urlpatterns = [
    path('api/students/', StudentListCreateAPIView.as_view(), name='student-list'),
]
