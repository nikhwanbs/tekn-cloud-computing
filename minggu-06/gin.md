<h1>Gin RESTful API</h1>
<h3>Install Gin</h3>
<img src="img/9.png">
<h3>Berikut source codenya</h3>
Buat koneksi Ke database

```package main

import (
	"github.com/jinzhu/gorm"
	"github.com/gin-gonic/gin"
	_ "github.com/jinzhu/gorm/dialects/mysql"
	"net/http"
)

var db *gorm.DB

func init() {
	var err error
	db, err =
		gorm.Open("mysql", "root:welcome1@tcp(127.0.0.1:3306)/golang?charset=utf8&parseTime=True&loc=Local")
	if err != nil {
		panic("Gagal Conect Ke Database")
	}
	db.AutoMigrate(&student{})
}
```