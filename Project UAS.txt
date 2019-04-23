#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <string.h>
#include <iostream>
#include <fstream>
using namespace std;

int kembali,bayar,no_op,no_nom,hrg_pulsa[5],nominal_pulsa[5],i,a,pil,pendapatan,terjual;
char cs[30],lagi,semula,cetak,init;

struct beli
{
    char nm_operator[10];
    int nom_beli,harga;
}pulsa;

void tampil_awal()
{
	cout<<"================================================="<<endl;
	cout<<"|                PENJUALAN PULSA                |"<<endl;
	cout<<"|                    I&Z CELL                   |"<<endl;
	cout<<"================================================="<<endl;
	cout<<" Costumer Service : "<<cs;
}

void tampil_operator()
{
	system("cls");
	cout<<"================================================="<<endl;
	cout<<"|              DAFTAR PRODUK PULSA              |"<<endl;
	cout<<"|                    I&Z CELL                   |"<<endl;
	cout<<"================================================="<<endl;
	cout<<"            1. Telkomsel"<<endl;
	cout<<"            2. Indosat"<<endl;
	cout<<"            3. XL"<<endl;
	cout<<"            4. Smart"<<endl;
	cout<<"            5. Three"<<endl;
}

void tampil_operator2()
{
	cout<<"\n            DAFTAR PRODUK"<<endl;
	cout<<"            1. Telkomsel"<<endl;
	cout<<"            2. Indosat"<<endl;
	cout<<"            3. XL"<<endl;
	cout<<"            4. Smart"<<endl;
	cout<<"            5. Three"<<endl;
	cout<<"            Pilih nomor operator : "; cin>>no_op;
}

void nominal()
{
	//system("cls");
	a=1;
	cout<<"================================================="<<endl;
	cout<<"|               DAFTAR NOMINAL PULSA            |"<<endl;
	cout<<"================================================="<<endl;
	for (i=0;i<5;i++)
	{
		cout<<"            "<<a;
		cout<<". "<<nominal_pulsa[i];
		cout<<" harga Rp "<<hrg_pulsa[i];
		cout<<endl;
		a++;
	}
}

void inisialisasi()
{
	nominal_pulsa[0]=5000;
	nominal_pulsa[1]=10000;
	nominal_pulsa[2]=25000;
	nominal_pulsa[3]=50000;
	nominal_pulsa[4]=100000;
	hrg_pulsa[0]=6000;
	hrg_pulsa[1]=11000;
	hrg_pulsa[2]=26000;
	hrg_pulsa[3]=51000;
	hrg_pulsa[4]=101000;
	pendapatan=0;
	terjual=0;
}

void t_lagi()
{
	int atas_menu(),menu_awal();

	cout<<"\nApakah ada transaksi lagi ? (Y/T)\n"; cin>>lagi;
	if (lagi=='Y'||lagi=='y')
	{atas_menu();
	menu_awal();}
	else if(lagi=='t'||lagi=='T')
	{system("cls");
	cout<<"=========================================================="<<endl;
	cout<<"| TERIMA KASIH TELAH MENGGUNAKAN PROGRAM PENJUALAN PULSA |"<<endl;
	cout<<"|                         I&Z CELL                       |"<<endl;
	cout<<"=========================================================="<<endl;
	cout<<" Sampai ketemu lagi "<<cs;}
	else
	{cout<<"\nMohon tuliskan Y atau T saja.\nUntuk karakter lain dan atau tulisan tidak diperbolehkan";
	t_lagi();}
}

void nota()
{
    ofstream nota;
    nota.open("nota.txt");
	system("cls");
	nota<<"\n\n";
	nota<<"==========================================================="<<endl;
	nota<<"|                        I&Z CELL	                  |"<<endl;
	nota<<"|  Jalan Perjuangan nomor 9, Kampung Terbaik, Kota Juara  |"<<endl;
	nota<<"==========================================================="<<endl;
	nota<<"|********************   NOTA PENJUALAN   *****************|"<<endl;
	nota<<" CS	: "<<cs;
	nota<<"\n***********************************************************"<<endl;
    nota<<"           Nama Produk		: "<<pulsa.nm_operator<<endl;
	nota<<"           Besar pulsa		: "<<pulsa.nom_beli<<endl;
	nota<<"           Harga		: Rp "<<pulsa.harga<<endl;
	nota<<"           ================================="<<endl;
	nota<<"           Pembayaran		: Rp "<<bayar<<endl;
	nota<<"           Kembali		: Rp "<<kembali<<endl;
	nota<<"           ================================="<<endl;
	nota<<"============================================================"<<endl;
	nota<<"        Terima kasih sudah berbelanja di I&Z Cell."<<endl;
	nota<<"          Semoga Anda puas dengan pelayanan kami."<<endl;
	nota<<"============================================================"<<endl;
	nota.close();
	system("cls");
	cout<<"\n\n";
	cout<<"==========================================================="<<endl;
	cout<<"|                        I&Z CELL	                  |"<<endl;
	cout<<"|  Jalan Perjuangan nomor 9, Kampung Terbaik, Kota Juara  |"<<endl;
	cout<<"==========================================================="<<endl;
	cout<<"|********************   NOTA PENJUALAN   *****************|"<<endl;
	cout<<" CS	: "<<cs;
	cout<<"\n***********************************************************"<<endl;
    cout<<"           Nama Produk		: "<<pulsa.nm_operator<<endl;
	cout<<"           Besar pulsa		: "<<pulsa.nom_beli<<endl;
	cout<<"           Harga		: Rp "<<pulsa.harga<<endl;
	cout<<"           ================================="<<endl;
	cout<<"           Pembayaran		: Rp "<<bayar<<endl;
	cout<<"           Kembali		: Rp "<<kembali<<endl;
	cout<<"           ================================="<<endl;
	cout<<"============================================================"<<endl;
	cout<<"        Terima kasih sudah berbelanja di I&Z Cell."<<endl;
	cout<<"          Semoga Anda puas dengan pelayanan kami."<<endl;
	cout<<"============================================================"<<endl;
	t_lagi();
}

void cek_bayar()
{
	int kembalian();
	if (bayar<pulsa.harga)
	{
		system("cls");
		cout<<"\nMaaf Anda membayar Rp "<<bayar<<endl;
		cout<<"Pembayaran anda kurang dari harga pulsa Rp "<<pulsa.harga<<endl;
		kembali=0;
		cout<<"\nUntuk mengingatkan,\nAnda telah membeli pulsa "<<pulsa.nm_operator;
		cout<<" dengan nominal pulsa "<<pulsa.nom_beli;
		cout<<" seharga Rp "<<pulsa.harga<<endl<<endl;
		cout<<"Silahkan masukkan nominal pembayaran: "; cin>>bayar;
		cek_bayar();}
	else
	{
        kembalian();
        pendapatan=pendapatan+pulsa.harga;
        terjual=terjual+1;
        cout<<"\n\nTransaksi berhasil.\nPendapatan sudah bertambah.\nApakah akan cetak nota ? (Y/T)\n"; cin>>cetak;
        if (cetak=='Y'||cetak=='y')
            nota();
        else if(cetak=='T'||cetak=='t')
            t_lagi();
        else
            cout<<"Maaf hanya boleh memasukkan karakter y atau t";
	}
}

void kembalian()
{
	kembali=0;
	kembali = bayar-pulsa.harga;
}

void rekap_pilih()
{
	cout<<"\nAnda membeli pulsa "<<pulsa.nm_operator;
    cout<<" dengan nominal pulsa "<<pulsa.nom_beli;
    cout<<" seharga Rp "<<pulsa.harga;
	cout<<"\n\nSilahkan masukkan nominal pembayaran: Rp "; cin>>bayar;
	kembalian();
	cek_bayar();
}

void pilihan_nom()
{
	if (no_nom==1)
	{pulsa.nom_beli=5000;
	pulsa.harga=hrg_pulsa[0];
	rekap_pilih();}
	else if(no_nom==2)
	{pulsa.nom_beli=10000;
	pulsa.harga=hrg_pulsa[1];
	rekap_pilih();}
	else if(no_nom==3)
	{pulsa.nom_beli=25000;
	pulsa.harga=hrg_pulsa[2];
	rekap_pilih();}
	else if(no_nom==4)
	{pulsa.nom_beli=50000;
	pulsa.harga=hrg_pulsa[3];
	rekap_pilih();}
	else if(no_nom==5)
	{pulsa.nom_beli=100000;
	pulsa.harga=hrg_pulsa[4];
	rekap_pilih();}
	else
	{cout<<"Maaf silahkan tuliskan nomor pulsanya(1 angka),\nbukan nominal pulsanya atau lainnya"<<endl;
	nominal();
	cout<<"\nMasukkan nomor nominal untuk operator "<<pulsa.nm_operator;
	cout<<" : "; cin>>no_nom;
	pilihan_nom();}
}

void hasil_pilih()
{
	switch (no_op)
	{
	case 1:
		{
			system("cls");
			nominal();
			strcpy(pulsa.nm_operator,"Telkomsel");
			cout<<"\nMasukkan nomor nominal untuk operator "<<pulsa.nm_operator;
			cout<<" : "; cin>>no_nom;
			pilihan_nom();
			break;
		}
	case 2:
		{
			system("cls");
			nominal();
			strcpy(pulsa.nm_operator,"Indosat");
			cout<<"\nMasukkan nomor nominal untuk operator "<<pulsa.nm_operator;
			cout<<" : "; cin>>no_nom;
			pilihan_nom();
			break;
		}
	case 3:
		{
			system("cls");
			nominal();
			strcpy(pulsa.nm_operator,"XL");
			cout<<"\nMasukkan nomor nominal untuk operator "<<pulsa.nm_operator;
			cout<<" : "; cin>>no_nom;
			pilihan_nom();
			break;
		}
	case 4:
		{
			system("cls");
			nominal();
			strcpy(pulsa.nm_operator,"Smart");
			cout<<"\nMasukkan nomor nominal untuk operator "<<pulsa.nm_operator;
			cout<<" : "; cin>>no_nom;
			pilihan_nom();
			break;
		}
	case 5:
		{
			system("cls");
			nominal();
			strcpy(pulsa.nm_operator,"Three");
			cout<<"\nMasukkan nomor nominal untuk operator "<<pulsa.nm_operator;
			cout<<" : "; cin>>no_nom;
			pilihan_nom();
			break;
		}
	default :
		{
			system("cls");
			cout<<"Nomor yang anda masukkan salah\n";
			tampil_operator2();
			hasil_pilih();
		break;
		}
	}
}

void penjualan()
{
	system("cls");
	tampil_awal();
	tampil_operator2();
	hasil_pilih();
}

void update_data()
{
	system("cls");
	cout<<"================================================="<<endl;
	cout<<"|      PROSES UPDATING HARGA PRODUK PULSA       |"<<endl;
	cout<<"|                    I&Z CELL                   |"<<endl;
	cout<<"================================================="<<endl;
	cout<<endl;
	int menu_awal();
	i=0;
	a=1;
	while (i<5)
	{
		cout<<"Harga pulsa "<<nominal_pulsa[i];
        cout<<" tadinya Rp "<<hrg_pulsa[i];
        cout<<" dirubah menjadi : "; cin>>hrg_pulsa[i];
		cout<<"Harga pulsa "<<nominal_pulsa[i];
		cout<<" sudah menjadi Rp "<<hrg_pulsa[i]<<endl<<endl;
		i++;
		a++;
	}
	system("cls");
	cout<<"====================================================="<<endl;
	cout<<"|                     TERIMA KASIH                  |"<<endl;
	cout<<"|       HARGA PRODUK SUDAH BERHASIL DIUPDATE!       |"<<endl;
	cout<<"====================================================="<<endl;
	nominal();
	menu_awal();
}

void atas_menu()
{
	system("cls");
	cout<<"================================================="<<endl;
	cout<<"|   SELAMAT DATANG DI PROGRAM PENJUALAN PULSA   |"<<endl;
	cout<<"|                    I&Z CELL                   |"<<endl;
	cout<<"================================================="<<endl;
	cout<<" Costumer Service/Pemakai program : "; cin>>cs;
}

void t_init()
{
	int menu_awal();
	cout<<"\nYakin akan mengembalikan data seperti semula?\n(semua data akan menjadi 0, termasuk pendapatan dan item terjual)\n(Y/T) --> ";
	cin>>init;
	if (init=='Y'||init=='y')
		{inisialisasi();
		system("cls");
		cout<<"Semua data sudah dikembalikan ke data semula..."<<endl<<endl;
		system("pause");
		atas_menu();
		menu_awal();}
	else if(init=='T'||init=='t')
		{system("cls");
		cout<<"\nPengembalian data dibatalkan. Silahkan dilanjutkan transaksi lainnya"<<endl<<endl;
		system("pause");
		atas_menu();
		menu_awal();}
	else
		{cout<<"\nMaaf hanya boleh memasukkan karakter y atau t"<<endl;
		t_init();}
}

void menu_awal()
{
	cout<<"\n========================================================"<<endl;
	cout<<"            1. Lihat produk"<<endl; // --> ke tampil_operator()
	cout<<"            2. Lihat harga produk"<<endl; // --> ke nominal()
	cout<<"            3. Penjualan"<<endl; //--> ke penjualan()
	cout<<"            4. Update harga produk"<<endl;//--> ke update_data()
	cout<<"            5. Kembalikan data seperti semula"<<endl;//--> ke inisialisasi()
	cout<<"            6. Lihat pendapatan"<<endl;//--> tampilkan pendapatan
	cout<<"            0. Keluar"<<endl;//--> keluar
	cout<<"\n      Anda akan(masukkan nomor menu) : " ; cin>>pil;
	switch (pil)
	{
	case 1:
		{
			tampil_operator();
			menu_awal();
		}break;
	case 2:
		{
			system("cls");
			nominal();
			menu_awal();
		}break;
	case 3: penjualan();break;
	case 4: update_data();break;
	case 5: t_init();break;
	case 6:
		{
			system("cls");
		cout<<"================================================="<<endl;
		cout<<"|   		HASIL PENJUALAN PULSA   	|"<<endl;
		cout<<"|                    I&Z CELL                   |"<<endl;
		cout<<"================================================="<<endl;
			cout<<"\n  Pendapatan sampai saat ini: Rp "<<pendapatan;
			cout<<"\n  Jumlah produk terjual sampai saat ini: "<<terjual;
			cout<<" item\n\n";
			system("pause");
			atas_menu();
			menu_awal();
		}break;
	case 0:
		{
			system("cls");
			cout<<"=========================================================="<<endl;
			cout<<"| TERIMA KASIH TELAH MENGGUNAKAN PROGRAM PENJUALAN PULSA |"<<endl;
			cout<<"|                         I&Z CELL                       |"<<endl;
			cout<<"=========================================================="<<endl;
			cout<<" Sampai ketemu lagi "<<cs;
			cout<<" :)"<<endl;
			system("pause");
		}break;
	default:
		{
			system("cls");
			cout<<"            Masukkan angka dari 1-5 dan 0"<<endl;
			menu_awal();
		}break;
	}
}

main()
{
    inisialisasi();
    login:
	char user[10];		//Deklarasi Variabel username utk login
	char pass[10];		//Deklarasi Variabel password utk login
	cout<<"==================================="<<endl;
    cout<<"|          Silakan Login          |"<<endl;
    cout<<"==================================="<<endl;
	cout<<" Username	: "; cin>>user;
    cout<<" Password	: "; cin>>pass;
if (strcmp(user,"agen")==0 && strcmp(pass,"12345")==0)
    {
        atas_menu();
        menu_awal();
    }
else
	{
		cout<<"\n\n Username atau Password salah, silakan login kembali"<<endl;
		goto login;
		return 0;
	}
}
