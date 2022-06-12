# ATM
#include "parayatirmaislemi.h"

#include <iostream>
#include <string>

#include "Veri/parayatirmaverisi.h"

using namespace std;

ParaYatirmaIslemi::ParaYatirmaIslemi(IslemDeposu &d) : depo(d) {}

void ParaYatirmaIslemi::yatir() {
  string hesapNo;
  double miktar;
  string tarih;

  cout << "Hesap Numarası     : ";
  cin >> hesapNo;
  cout << "Yatırılacak Miktar : ";
  cin >> miktar;
  cout << "Tarih              : ";
  cin >> tarih;

  ParaYatirmaVerisi pyv(tarih, miktar, hesapNo);

  depo.paraYatir(pyv);
}
#ifndef PARAYATIRMAISLEMI_H
#define PARAYATIRMAISLEMI_H

#include "Veri/islemdeposu.h"

class ParaYatirmaIslemi {
public:
  ParaYatirmaIslemi(IslemDeposu &d);

  void yatir();

private:
  IslemDeposu &depo;
};

#endif // PARAYATIRMAISLEMI_H
#include "hesaphareketleriislemi.h"

HesapHareketleriIslemi::HesapHareketleriIslemi()
{

}
#ifndef HESAPHAREKETLERIISLEMI_H
#define HESAPHAREKETLERIISLEMI_H


class HesapHareketleriIslemi
{
public:
    HesapHareketleriIslemi();
};

#endif // HESAPHAREKETLERIISLEMI_H
#include "menu.h"

#include "hesaphareketleriislemi.h"
#include "paracekmeislemi.h"
#include "parayatirmaislemi.h"

#include <iostream>

Menu::Menu() {}

void Menu::calistir() {
  while (true) {
    int secim;
    cout << "HOŞ GELDİNİZ" << endl
         << "BİR İŞLEM SEÇİN " << endl
         << "[1] PARA ÇEKME " << endl
         << "[2] PARA YATIRMA " << endl
         << "[3] HESAP HAREKETLERİ " << endl
         << "[4] ÇIKIŞ" << endl
         << " SEÇİMİNİZ :";
    cin >> secim;
    if (secim == 1) {
      ParaCekmeIslemi islem(depo);
      islem.cek();
    } else if (secim == 2) {
      ParaYatirmaIslemi islem(depo);
      islem.yatir();
    } else if (secim == 3) {
      cout << "HENÜZ HAZIR DEĞİL!" << endl;
    } else {
      break;
    }
  }
}
ifndef MENU_H
#define MENU_H

#include "Veri/islemdeposu.h"

class Menu {
public:
  Menu();

  void calistir();

private:
  IslemDeposu depo;
};

#endif // MENU_H
#ifndef PARACEKMEISLEMI_H
#define PARACEKMEISLEMI_H

#include <Veri/islemdeposu.h>

class ParaCekmeIslemi {
public:
  ParaCekmeIslemi(IslemDeposu &d);

  void cek();

private:
  IslemDeposu &depo;
};

#endif // PARACEKMEISLEMI_H
#include "paracekmeislemi.h"

#include <iostream>
#include <string>

#include "Veri/paracekmeverisi.h"

using namespace std;

ParaCekmeIslemi::ParaCekmeIslemi(IslemDeposu &d) : depo(d) {}

void ParaCekmeIslemi::cek() {
  string hesapNo;
  double miktar;
  string tarih;

  cout << "Hesap Numarası     : ";
  cin >> hesapNo;

  double bakiye = depo.bakiye(hesapNo);

  cout << "Bakiyeniz " << bakiye << endl;
  cout << "Çekilecek Miktar   : ";
  cin >> miktar;
  while (miktar > bakiye) {
    cerr << "YETERSİZ BAKİYE..." << endl;
    cout << "Çekilecek Miktar   : ";
    cin >> miktar;
    if (miktar < 0)
      return;
  }
  cout << "Tarih              : ";
  cin >> tarih;

  ParaCekmeVerisi pyv(tarih, miktar, hesapNo);

  depo.paraCek(pyv);
}

  
