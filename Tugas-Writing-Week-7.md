# React JS Lanjutan

# React Router

> Router adalah standar ruting yang dimana digunakan sebagai librery rooter untuk mengarahkan dari page ke 1 ke page yang lain yang dimana page tersebut diarahkan menggunakan URL.

### Basic Installation

> Untuk menambahkan React Router ke proyek yang sudah ada, hal pertama yang harus Anda lakukan adalah menginstal dependensi yang diperlukan dengan alat pilihan antara lain:
> NPM :
> $ npm install react-router-dom@6

> Setelah proyek Anda diatur dan React Router diinstal sebagai dependensi, buka src/index.js di editor teks Anda. Impor BrowserRouter dari react-router-dom di dekat bagian atas file Anda dan bungkus aplikasi Anda dalam <BrowserRouter>

**Contoh Penulisannya configurasi router**

    import * as React from "react";
    import ReactDOM from "react-dom/client";
    import {BrowserRouter,Routes,Route,} from "react-router-dom";
    import "./index.css";
    import App from "./App";
    import reportWebVitals from "./reportWebVitals";

    const root = ReactDOM.createRoot(
    document.getElementById("root")
    );
    root.render(
    <React.StrictMode>
        <BrowserRouter>
            <Routers>
                <App/>
            </Routers>
        </BrowserRouter>
    </React.StrictMode>
    );

## Navigation

> Gunakan 'Link' untuk mengizinkan pengguna mengubah URL atau gunakan Navigasi untuk melakukannya sendiri (seperti setelah pengiriman formulir)

    import { Link } from "react-router-dom";

    function Home() {
    return (
        <div>
        <h1>Home</h1>
        <nav>
            <Link to="/">Home</Link> |{" "}
            <Link to="about">About</Link>
        </nav>
        </div>
    );
    }

## Nested Routers

> Sebagian besar tata letak Anda digabungkan ke segmen URL dan React Router mencakup ini sepenuhnya.Rute dapat bersarang di dalam satu sama lain, dan jalurnya juga akan bersarang (anak mewarisi induknya).

    function App() {
    return (
        <Routes>
        <Route path="invoices" element={<Invoices />}>
            <Route path=":invoiceId" element={<Invoice />} />
            <Route path="sent" element={<SentInvoices />} />
        </Route>
        </Routes>
    );
    }

## **Browser Router**

> BrowserRouter adalah antar muka yang direkomendasikan untuk menjalankan React Router di browser web. BrowserRouter menyimpan lokasi saat ini di bilah alamat browser menggunakan URL bersih dan bernavigasi menggunakan tumpukan riwayat bawaan browser.

<BrowserRouter window> default untuk menggunakan defaultView dokumen saat ini, tetapi juga dapat digunakan untuk melacak perubahan ke URL jendela lain, dalam iframe, misalnya:

    import * as React from "react";
    import * as ReactDOM from "react-dom";
    import { BrowserRouter } from "react-router-dom";

    ReactDOM.render(
    <BrowserRouter>
        {/* The rest of your app goes here */}
    </BrowserRouter>,
    root
    );

## Hooks

> Hooks adalah tambahan baru di React 16.8. Mereka memungkinkan Anda menggunakan status dan fitur React lainnya tanpa menulis kelas.

    import React, { useState } from 'react';

    function Example() {
    // Declare a new state variable, which we'll call "count"
    const [count, setCount] = useState(0);

    return (
        <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>
            Click me
        </button>
        </div>
    );
    }

## State Management

> State Management adalah pengaturan data agar data tersebut bisa digunakan untuk rius eble, bisa juga mengatur data-data yang dapat di share untuk komponent yang lain.Dalam pengantar singkat untuk Redux ini, kita akan membahas konsep utama: reducers, actions, action creators and store.

1.  Reducers
    > Reducer menentukan bagaimana status aplikasi berubah sebagai respons terhadap tindakan yang dikirim ke store.
2.  actions
    > actions adalah objek JavaScript biasa yang mewakili muatan informasi yang mengirimkan data dari aplikasi Anda ke store Anda. actions memiliki jenis dan muatan opsional.
3.  action creators

    > Di Redux, pembuat tindakan adalah fungsi yang mengembalikan objek actions. Bagian status yang baru dikembalikan kemudian disalurkan ke status aplikasi, yang kemudian disalurkan kembali ke aplikasi React kami, yang kemudian menyebabkan semua komponen kami dirender ulang.Jadi katakanlah pengguna mengklik tombol, lalu kita memanggil pembuat tindakan yang merupakan fungsi yang mengembalikan actions. Tindakan itu memiliki jenis yang menjelaskan jenis actions yang baru saja dipicu. Berikut adalah contoh pembuat tindakan:

         export function addTodo({ task }) {
         return {
             type: 'ADD_TODO',
             payload: {
             task,
             completed: false
             },
         }
         }

         // example returned value:
         // {
         //   type: 'ADD_TODO',
         //   todo: { task: '🛒 get some milk', completed: false },
         // }

4.  store
    > Di Redux, store mengacu pada objek yang menyatukan tindakan (yang mewakili apa yang terjadi) dan reduksi (yang memperbarui status sesuai dengan tindakan tersebut). Hanya ada satu store dalam aplikasi Redux.

store memiliki beberapa tugas:

- Izinkan akses ke status melalui getState().
- Izinkan status diperbarui melalui pengiriman (tindakan).
- Memegang seluruh status aplikasi.
- Mendaftar pendengar menggunakan berlangganan (pendengar).
- Batalkan pendaftaran pendengar melalui fungsi yang dikembalikan oleh berlangganan (pendengar).

> Pada dasarnya semua yang kita butuhkan untuk membuat store adalah reduksi. Kami menyebutkan combineReducers untuk menggabungkan beberapa reduksi menjadi satu. Sekarang, untuk membuat store, kami akan mengimpor combineReducers dan meneruskannya ke createStore:

    import { createStore } from 'redux';
    import todoReducer from './reducers';

    const store = createStore(todoReducer);

> Kemudian mengirimkan tindakan di aplikasi kami menggunakan dispatch metode pengiriman store seperti:

    store.dispatch(addTodo({ task: '📖 Read about Redux'}));
    store.dispatch(addTodo({ task: '🤔 Think about meaning of life' }));
    // ...
