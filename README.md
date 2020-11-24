# Tugas9-IBD-RifqiAnugrah-195410238
Tugas 9 Infrastruktur Big Data - ENDPOINT BACKEND DENGAN BAHASA PEMOGRAMAN RUST

Dilakukan proses operasi CRUD sederhana untuk mengelola Data Hero, dibutuhkan beberapa data pendukung yaitu :
Create:POST /hero
Read: GET /heroes
Update: PUT /hero/:id
Delete: DELETE /hero/:id

Sebelum masuk ke pembuatan Endpoint, perlu ditekankan dalam proses pembuatannya digunakan JSON sebagai sarana utama dalam melakukan proses pertukaran data. 
Dibutuhkan tambahan kode perintah pada Cargo.toml yaitu :
[package]
name = "hero-api"
version = "0.1.0"
authors = ["sean"]

[dependencies]
rocket = "0.3.6"
rocket_codegen = "0.3.6"
serde = "1.0"
serde_json = "1.0"
serde_derive = "1.0"

[dependencies.rocket_contrib]
version = "*"
default-features = false
features = ["json"]


Setelah itu dilakukan proses pembuatan Hero Model dengan menambahkan kode perintah
src/hero.rs dan Serialize and Deserialize, kode perintah tersebut berguna untuk membuat model yang telah dibuat dapat diesktrasi dan dikonversi ke JSON.

#![feature(plugin)]
#![plugin(rocket_codegen)]

extern crate rocket;
#[macro_use] extern crate rocket_contrib;
#[macro_use] extern crate serde_derive;

use rocket_contrib::{Json, Value};

mod hero;
use hero::{Hero};

#[post("/", data = "<hero>")]
fn create(hero: Json<Hero>) -> Json<Hero> {
    hero
}

#[get("/")]
fn read() -> Json<Value> {
    Json(json!([
        "hero 1", 
        "hero 2"
    ]))
}

#[put("/<id>", data = "<hero>")]
fn update(id: i32, hero: Json<Hero>) -> Json<Hero> {
    hero
}

#[delete("/<id>")]
fn delete(id: i32) -> Json<Value> {
    Json(json!({"status": "ok"}))
}

fn main() {
    rocket::ignite()
        .mount("/hero", routes![create, update, delete])
        .mount("/heroes", routes![read])
        .launch();
        
        

Pada kode perintah diatas, disertakan dependensi baru dan dilakukan proses mereferensikan tipe hero, serta dilakukan proses penarikan JSON dan VALUE dari rocket_contrib, hal ini dilakukan untuk mempermudah proses menangani permintaan dan tanggapan pada JSON

#[macro_use] extern crate rocket_contrib;
#[macro_use] extern crate serde_derive;
use rocket_contrib::{Json, Value};
mod hero;
use hero::{Hero};

Daftar Pustaka : https://medium.com/sean3z/building-a-restful-crud-api-with-rust-1867308352d8
