#include <iostream>
#include <fstream>
#include <string>
#include <bits/stdc++.h>
#include <iomanip>
#include <algorithm>
using namespace std;

struct Mahasiswa{
    string namaAwal, namaAkhir, nama;
    string prodi = "S1 Ilmu Komputer";
    string semester = "Semester 1";
    string matkul[9]= {"Fisika Dasar 1","Kimia Dasar 1","Pemrograman","Kalkulus 1","Agama","Bahasa Indonesia","Aljabar Linear","Logika Informatika","Prak Pemrograman"};
    string grade[9];
    unsigned int id;
    unsigned int niu;
    unsigned int rank;
    short sks[9] = {3, 3, 3, 3, 2, 2, 2, 2, 1};
    float nilai[9];
    float nilaiSks[9];
    float ipkMatkul[9];
    float totalNilai = 0;
    float ipk;
};

int getOption();
void inputData(ofstream &myFile, int &idmhs);
void writeData(ofstream &myFile, Mahasiswa &mahasiswa);
void readData(ifstream &inputFile, Mahasiswa mahasiswa[], int &jumlah);
void printRank(Mahasiswa mahasiswa[], int &jumlah);
void printRapot(Mahasiswa mahasiswa[], int &jumlah);
int cariJumlah(ifstream &inputFile);
int idAkhir(ifstream &inputFile);
void deleteData(ofstream &outputFile, int jumlah, Mahasiswa mahasiswa[]);
void deleteAll(ofstream &outputFile);
bool compareRank(Mahasiswa a, Mahasiswa b);
bool compareId(Mahasiswa a, Mahasiswa b);
void searchRank(Mahasiswa mahasiswa[], int &jumlah);
int searchNiu(Mahasiswa mahasiswa[], int &jumlah);


int main(){
    ofstream outputFile;
    ifstream inputFile;
    outputFile.open("data.txt", ios::app);
    inputFile.open("data.txt", ios::in);
    int jumlah = cariJumlah(inputFile);
    int idmhs = idAkhir(inputFile);
    Mahasiswa mahasiswa[jumlah];
    readData(inputFile, mahasiswa, jumlah);
    pilihOpsi:
    int opsi = getOption();
    char is_continue;
	
    switch (opsi){
        case 1:
            inputData(outputFile, idmhs);
            break;
        case 2:
            printRank(mahasiswa, jumlah);
            break;
        case 3:
            printRapot(mahasiswa, jumlah);
            break;
        case 4:
            searchRank(mahasiswa, jumlah);
            break;
        case 5:
            int hapusPilih;
            cout << "Hapus data" << endl;
            cout << "1.Hapus satu berdasarkan id" << endl;
            cout << "2.Reset" << endl;
            cin >> hapusPilih;
            deleteAll(outputFile);
            if(hapusPilih==2){
                cout << "Database telah berhasil direset" << endl;
            } else if(hapusPilih==1){
                deleteData(outputFile, jumlah, mahasiswa);
            } else{
                cout << "Perintah tidak dikenali" << endl;
            }
            cout << endl << "Anda mungkin dapat merestart program untuk melihat perubahan" << endl;
            break;
        default:
            cout << "Perintah tidak dikenali" << endl;
    }
    cout << endl << "Apakah Anda ingin exit program? [y/n]  ";
    cin >> is_continue;
    if(is_continue == 'n'){
        goto pilihOpsi;
    }
    inputFile.close();
    outputFile.close();
    cout << "Akhir Program" << endl;
    return 0;
}

int getOption(){
    int opsi;
    system("cls");
    cout << "Welcome" << endl << endl;
    cout << "Pilih program" << endl;
    cout << "1.Input mahasiswa" << endl;
    cout << "2.Tampilkan rangking" << endl;
    cout << "3.Tampilkan rapot" << endl;
    cout << "4.Cari data" << endl;
    cout << "5.Hapus data" << endl;
    cout << "Pilih [1-5]: ";
    cin >> opsi;
    cout << endl;
    cin.ignore();
    return opsi;
}

void readData(ifstream &inputFile, Mahasiswa mahasiswa[], int &jumlah){
    string buffer;
    for(int i=0;i<jumlah;i++){
        float jumlahNilaiSks=0;
        int jumlahSks=21;
        inputFile >> mahasiswa[i].id;
        for(int j=0;j<2;j++){
            inputFile >> buffer;
            if(buffer!="-"){
                mahasiswa[i].nama += buffer + " ";
            }
            if(j==0){
                mahasiswa[i].namaAwal = buffer;
            } else if(j==1){
                mahasiswa[i].namaAkhir = buffer;
            }
        }
        inputFile >> mahasiswa[i].niu;
        inputFile >> mahasiswa[i].nilai[0];
        inputFile >> mahasiswa[i].nilai[1];
        inputFile >> mahasiswa[i].nilai[2];
        inputFile >> mahasiswa[i].nilai[3];
        inputFile >> mahasiswa[i].nilai[4];
        inputFile >> mahasiswa[i].nilai[5];
        inputFile >> mahasiswa[i].nilai[6];
        inputFile >> mahasiswa[i].nilai[7];
        inputFile >> mahasiswa[i].nilai[8];
        for(int j=0;j<9;j++){
            if(mahasiswa[i].nilai[j]>90){
                mahasiswa[i].grade[j]="A";
                mahasiswa[i].ipkMatkul[j] = 4;
                mahasiswa[i].nilaiSks[j]= mahasiswa[i].sks[j]*4;
            } else if(mahasiswa[i].nilai[j]>85){
                mahasiswa[i].grade[j]="A-";
                mahasiswa[i].ipkMatkul[j] = 3.75;
                mahasiswa[i].nilaiSks[j]= mahasiswa[i].sks[j]*3.75;
            } else if(mahasiswa[i].nilai[j]>80){
                mahasiswa[i].grade[j]="A/B";
                mahasiswa[i].ipkMatkul[j] = 3.5;
                mahasiswa[i].nilaiSks[j]= mahasiswa[i].sks[j]*3.5;
            } else if(mahasiswa[i].nilai[j]>75){
                mahasiswa[i].grade[j]="B+";
                mahasiswa[i].ipkMatkul[j] = 3.25;
                mahasiswa[i].nilaiSks[j]= mahasiswa[i].sks[j]*3.25;
            } else if(mahasiswa[i].nilai[j]>70){
                mahasiswa[i].grade[j]="B";
                mahasiswa[i].ipkMatkul[j] = 3;
                mahasiswa[i].nilaiSks[j]= mahasiswa[i].sks[j]*3;
            } else if(mahasiswa[i].nilai[j]>65){
                mahasiswa[i].grade[j]="B-";
                mahasiswa[i].ipkMatkul[j] = 2.75;
                mahasiswa[i].nilaiSks[j]= mahasiswa[i].sks[j]*2.75;
            } else if(mahasiswa[i].nilai[j]>60){
                mahasiswa[i].grade[j]="B/C";
                mahasiswa[i].ipkMatkul[j] = 2.5;
                mahasiswa[i].nilaiSks[j]= mahasiswa[i].sks[j]*2.5;
            } else if(mahasiswa[i].nilai[j]>55){
                mahasiswa[i].grade[j]="C+";
                mahasiswa[i].ipkMatkul[j] = 2.25;
                mahasiswa[i].nilaiSks[j]= mahasiswa[i].sks[j]*2.25;
            } else if(mahasiswa[i].nilai[j]>50){
                mahasiswa[i].grade[j]="C";
                mahasiswa[i].ipkMatkul[j] = 2;
                mahasiswa[i].nilaiSks[j]= mahasiswa[i].sks[j]*2;
            } else if(mahasiswa[i].nilai[j]>45){
                mahasiswa[i].grade[j]="C-";
                mahasiswa[i].ipkMatkul[j] = 1.75;
                mahasiswa[i].nilaiSks[j]= mahasiswa[i].sks[j]*1.75;
            } else if(mahasiswa[i].nilai[j]>40){
                mahasiswa[i].grade[j]="C/D";
                mahasiswa[i].ipkMatkul[j] = 1.5;
                mahasiswa[i].nilaiSks[j]= mahasiswa[i].sks[j]*1.5;
            } else if(mahasiswa[i].nilai[j]>35){
                mahasiswa[i].grade[j]="D+";
                mahasiswa[i].ipkMatkul[j] = 1.25;
                mahasiswa[i].nilaiSks[j]= mahasiswa[i].sks[j]*1.25;
            } else if(mahasiswa[i].nilai[j]>30){
                mahasiswa[i].grade[j]="D";
                mahasiswa[i].ipkMatkul[j] = 1;
                mahasiswa[i].nilaiSks[j]= mahasiswa[i].sks[j]*1;
            } else{
                mahasiswa[i].grade[j]='E';
                mahasiswa[i].ipkMatkul[j] = 0;
                mahasiswa[i].nilaiSks[j]= mahasiswa[i].sks[j]*0;
            }
            jumlahNilaiSks += mahasiswa[i].nilaiSks[j];
            mahasiswa[i].totalNilai+=mahasiswa[i].nilaiSks[j];
        }
        mahasiswa[i].ipk = jumlahNilaiSks/jumlahSks;
    }
    sort(mahasiswa, mahasiswa+jumlah, compareRank);
    for (int i=0; i<jumlah; i++){
		mahasiswa[i].rank = i+1;
	}
}


void inputData(ofstream &outputFile, int &idmhs){
    int n;
    string temp;
    cout << "Input mahasiswa" << endl;
    cout << "Tentukan jumlah mahasiswa ";
    cin >> n;
    Mahasiswa mahasiswa[n];
    cout << endl;
    for(int i=0;i<n;i++){
        mahasiswa[i].id = idmhs+i+1;
        cout << "ID Mahasiswa: " << mahasiswa[i].id << endl;
        cout << "Input nama depan mahasiswa: ";
        cin >> mahasiswa[i].namaAwal;
        cout << "Input nama belakang (Apabila tidak ada isi dengan \"-\"): ";
        cin >> mahasiswa[i].namaAkhir;
        cout << "Input NIU mahasiswa: ";
        cin >> mahasiswa[i].niu;
        cout << "Input nilai Fisika Dasar 1: ";
        cin >> mahasiswa[i].nilai[0];
        cout << "Input nilai Kimia Dasar 1: ";
        cin >> mahasiswa[i].nilai[1]; 
        cout << "Input nilai Pemrograman: ";
        cin >> mahasiswa[i].nilai[2]; 
        cout << "Input nilai Kalkulus 1: ";
        cin >> mahasiswa[i].nilai[3]; 
        cout << "Input nilai Agama: ";
        cin >> mahasiswa[i].nilai[4]; 
        cout << "Input nilai Bahasa Indonesia: ";
        cin >> mahasiswa[i].nilai[5]; 
        cout << "Input nilai Aljabar Linear: ";
        cin >> mahasiswa[i].nilai[6]; 
        cout << "Input nilai Logika Informatika: ";
        cin >> mahasiswa[i].nilai[7]; 
        cout << "Input nilai Praktikum Pemrograman: ";
        cin >> mahasiswa[i].nilai[8];
        writeData(outputFile, mahasiswa[i]);
        cout << endl;
    }
    cout << "Data berhasil diinput" << endl;
    cout << endl << "Anda mungkin dapat merestart program untuk melihat perubahan" << endl;
}

void writeData(ofstream &outputFile, Mahasiswa &mahasiswa){
    outputFile << mahasiswa.id << "\t";
    outputFile << mahasiswa.namaAwal << "\t";
    outputFile << mahasiswa.namaAkhir << "\t";      
    outputFile << mahasiswa.niu << "\t";
    outputFile << mahasiswa.nilai[0] << "\t";
    outputFile << mahasiswa.nilai[1] << "\t";
    outputFile << mahasiswa.nilai[2] << "\t";
    outputFile << mahasiswa.nilai[3] << "\t";
    outputFile << mahasiswa.nilai[4] << "\t";
    outputFile << mahasiswa.nilai[5] << "\t";
    outputFile << mahasiswa.nilai[6] << "\t";
    outputFile << mahasiswa.nilai[7] << "\t";
    outputFile << mahasiswa.nilai[8] << "\n";
}

int cariJumlah(ifstream &inputFile){
    string buffer;
    int jumlah = 0;
    while(!inputFile.eof()){
        getline(inputFile, buffer);
        jumlah++;
    }
    inputFile.close();
    inputFile.open("data.txt", ios::in);
    return jumlah-1;
}

int idAkhir(ifstream &inputFile){
    string buffer;
    int id=0, ids;
    do{
        inputFile >> ids;
        if(ids>id && ids<1000){
            id=ids;
        }
        getline(inputFile, buffer);
    } while(!inputFile.eof());
    inputFile.close();
    inputFile.open("data.txt", ios::in);
    return id;
}

void deleteData(ofstream &outputFile, int jumlah, Mahasiswa mahasiswa[]){
    int id;
    cout << "Input id: ";
    cin >> id;
    for(int i=0;i<jumlah;i++){
        if(id!=mahasiswa[i].id){
            writeData(outputFile, mahasiswa[i]);            
        }
    }
}

void deleteAll(ofstream &outputFile){
    outputFile.close();
    outputFile.open("data.txt", ios::trunc);
}

void printRapot(Mahasiswa mahasiswa[], int &jumlah){
    int j = searchNiu(mahasiswa, jumlah);
	system("cls");
	cout << "\t\t\t   KARTU HASIL STUDI" << endl;
	cout << "\t\t\tSemester Gasal 2022/2023" << endl;
	cout << "\nNama\t: " << mahasiswa[j].nama;
	cout << "\t\t\tIP Semester  : " << mahasiswa[j].ipk << endl;
	cout << "NIU\t: " << mahasiswa[j].niu << endl;
	cout << "Prodi\t: S1 ILMU KOMPUTER\n\n";
	cout << "No\t| Mata Kuliah\t\t| SKS\t| Nilai\t| Bobot\t| Nilai SKS |" << endl;
	cout << "--------------------------------------------------------------------" << endl;
	for(int i=0; i<9; i++){
		cout << i+1 << "\t| ";
		if(i==1||i==2||i==3) cout << mahasiswa[j].matkul[i] << "\t\t| ";
		else if(i==4) cout << mahasiswa[j].matkul[i] << "\t\t\t| ";
		else cout << mahasiswa[j].matkul[i] << "\t| ";
		cout << mahasiswa[j].sks[i] << "\t| ";
		cout << mahasiswa[j].grade[i] << "\t| ";
		cout << mahasiswa[j].ipkMatkul[i] << "\t| ";
		cout << mahasiswa[j].nilaiSks[i] << endl;
	}
	cout << "--------------------------------------------------------------------" << endl;
	cout << "\t\t\t\t\tJumlah nilai\t| " << mahasiswa[j].totalNilai << endl;
}

void printRank(Mahasiswa mahasiswa[], int &jumlah){
    sort(mahasiswa, mahasiswa+jumlah, compareRank);
    cout<<"PEMERINGKATAN MAHASISWA CS UGM SEMESTER GASAL 2022/2023"<<endl;
	cout<<"_______________________________________________________\n\n";
    cout<<"Rank\t";
    cout<<"Nama\t\t";
    cout<<"Program Studi\t\t";
    cout<<"NIU\t";
    cout<<"IPK";
    cout<<endl;
    
    for (int i=0; i<jumlah; i++){
    cout<<setw(3);
    cout<<mahasiswa[i].rank<<"\t";
    cout<<mahasiswa[i].namaAwal<<"\t\t";
    cout<<mahasiswa[i].prodi << "\t";
    cout<<mahasiswa[i].niu << "\t";
    cout<<mahasiswa[i].ipk;
    cout<<endl;
    }
    cout << "Jumlah mahasiswa: " << jumlah << endl;
    
}

bool compareRank(Mahasiswa a, Mahasiswa b){
	if (a.ipk != b.ipk) {
		return a.ipk > b.ipk;
	} else {
		return a.nama < b.nama;
	}
}

bool compareId(Mahasiswa a, Mahasiswa b){
	if (a.id != b.id) {
		return a.id > b.id;
	} else {
		return a.nama < b.nama;
	}
}

void searchRank(Mahasiswa mahasiswa[], int &jumlah){
    sort(mahasiswa, mahasiswa+jumlah, compareRank);
    cout<<"PENCARIAN DATA MAHASISWA CS UGM 2022/2023\n";
    cout<<"_________________________________________\n\n";
    int target,mid;
    int left;
    int right;
    left=0;
    right=jumlah-1;
    cout<<"Mahasiswa pada peringkat : ";
    cin>>target;

    
    while (left <= right){
        mid = left + (right-left)/2;
        if (mahasiswa[mid].rank == target){
            cout<<"\nData mahasiswa ditemukan.\n";
            cout<<"Nama : "<<mahasiswa[mid].nama<<endl;
            cout<<"NIU  : "<<mahasiswa[mid].niu<<endl;
            cout<<"IPK  : "<<mahasiswa[mid].ipk<<endl;
            break;
        } else if (mahasiswa[mid].rank < target) {
            left = mid + 1;
        } else if (mahasiswa[mid].rank> target) {
            right = mid - 1;
        }
    }
    
    if(left>right){
        cout<<"Data mahasiswa tidak ditemukan."
            <<"Permintaan Anda melampaui jumlah mahasiswa yang ada di CS UGM 2022/2023";
    }
}


int searchNiu(Mahasiswa mahasiswa[], int &jumlah){
    int target, mid;
    int left, right;
    left=0;
    right=jumlah-1;
    cout<<"Mahasiswa dengan NIU : ";
    cin>>target;
    
    for(int i=0;i<jumlah;i++){
        if(mahasiswa[i].niu==target){
            return i;
        }
    }
    cout << "Data tidak ditemmukan" << endl;
    return -1;
}
