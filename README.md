# Sth-useless
#include <iostream>
#include <string.h>


using namespace std;

int N;
int k;
struct cars
       {
           char marka[40];
           char cvqt[20];
           float cena;
           char kod[8];
           char *klas;//klas na  kola v tekstov vid
           char data[6];//poslednite 6 simvola ot koda
           };
           
cars S[200],SF[200];


void vhod(int m)
     {
     cout<<"\nDanni za kolite\n";
     cout<<"------------------------------";
     for (int i=0;i<m;i++)  
         {
         cout<<" \nMarka na kola "<<i+1<<" ";
       cin.getline(S[i].marka,40);
         
         cout<<"\n Cvqt na kola "<<i+1<<" ";
         cin>>S[i].cvqt;
         
         cout<<" Cena za naem za edin den na kola "<<i+1<<" ";
         cin>>S[i].cena;    
         
         cout<<" Kod na kola "<<i+1<<" ";
         cin>>S[i].kod;
         //podgotovka na pole data - neobhodimo e v Uslovie 3
         for (int j=0;j<6;j++)
         {S[i].data[j]=S[i].kod[j+2];}
         
     cin.ignore();
  
         }
     }
     
   float suma(int m)//izchislyava sumata na vsichki koli
   {
         float s=0;
         for (int i=0;i<m;i++)  
         {s=s+S[i].cena;}
         return s;
         }
         
void izhod(int m)
{
    
       cout<<"\n\nSPISYK NA VSICHKI KOLI:\n";
      for (int i=0;i<m;i++)
      { 
         
       cout<<"\n"<<S[i].marka; 
  // tuk se podgotvya i pole klas za Uslovie 3
        switch (S[i].kod[1])         
        {
        case '1': {cout<<", malka";S[i].klas="malka";break;}
        case '2': {cout<<", kompaktna";S[i].klas="kompaktna";break;}
        case '3': {cout<<", sredna";S[i].klas="sredna";break;}
        case '4': {cout<<", van";S[i].klas="van";break;}
        case '5': {cout<<", djip";S[i].klas="djip";break;}
        };  
        cout<<", "<<S[i].cvqt;
        cout<<", "<<S[i].cena;
        cout<<", "<<S[i].kod[2]<<S[i].kod[3]<<"."<<S[i].kod[4]
        <<S[i].kod[5]<<"."<<S[i].kod[6]<<S[i].kod[7]<<".";
                   } 
             
}  
               

 //sledvashtata funkciya podgotvya masiv samo ot koli "audi" i "bmw", koito ne sa vyrnati na 14.08.2008
void filter(int m)
{
      
    k=0;
     for (int i=0;i<m;i++)
     {
  
   if(!strstr(S[i].kod,"140808")) 
        
    {
         if  ( (strstr(S[i].marka,"bmw")||strstr(S[i].marka,"audi")) )
            {SF[k]=S[i];k++;}
     }
}   
 
}


 //funkciya za sortirane po dvata kriteriya, ukazani v Uslovie 3 
void sort_klas()
 
 {
      cars r;
      for(int i=0;i<k;i++)
      for (int j=k-1;j>i;j--)
      if ((strcmp(SF[j-1].klas,SF[j].klas)>0)||(strcmp(SF[j-1].klas,SF[j].klas)==0)
      &&(SF[j-1].data<SF[j].data))
      {r=SF[j-1];SF[j-1]=SF[j];SF[j]=r;}
  }


            

void izhod2()
{
     cout<<"\n\nSPISYK NA KOLI AUDI i BMW, ne vyrnati na 14.08.2008 g.\n"; 
      for (int i=0;i<k;i++)
      { 
          cout<<"\n"<<SF[i].marka;             
        switch (SF[i].kod[1])         
        {
        case '1': cout<<", malka";break;
        case '2': cout<<", kompaktna";break;
        case '3': cout<<", sredna";break;
        case '4': cout<<", van";break;
        case '5': cout<<", djip";break;
        };  
        cout<<", "<<SF[i].cvqt;
        cout<<", "<<SF[i].cena;
        cout<<", "<<SF[i].kod[2]<<SF[i].kod[3]<<"."<<SF[i].kod[4]<<SF[i].kod[5]<<"."<<SF[i].kod[6]<<SF[i].kod[7]<<".";
                }        

}  
      
void sort(int m)      
 
 {
      cars r;     
      for(int i=0;i<m;i++)    
      for (int j=m-1;j>i;j--) 
      if (strcmp(S[j-1].marka,S[j].marka)>0)    
      {
      r=S[j-1];                             
      S[j-1]=S[j];                          
      S[j]=r;                               
      }
  }
       
     
int main()
{
    float sredna_cena,sr1,sr2,sr3;
    int n1,n2,n3;
    do
    {N=0;cout<<"n1=";cin>>n1;
    cout<<"n2=";cin>>n2;
    cout<<"n3=";cin>>n3;
    N=n1+n2+n3;
}
while (N<0||N>200);
cout<<"------------------------------";
cout<<"\nPYRVA FIRMA:\n";
cout<<"------------------------------";
cin.ignore();
    vhod(n1);
    sort(n1); // podgotovka Uslovie 2
   izhod(n1);      // za vsichki koli - Uslovie 2
  filter(n1);// podgotovka na Uslovie 3 - masiv SF
  sort_klas();//podgotovka na Uslovie 3 - podrezhda masiva SF po klas i data na vryshtane
izhod2();// spisyk na koli - Uslovie 3
sr1=suma(n1)/n1;
cout<<"\n\nSrednata stojnost na kolite e = "<<sr1<<" leva.";
 cout<<"\n------------------------------";
 cout<<"\nVTORA FIRMA:\n";
cout<<"------------------------------";
//cin.ignore();
    vhod(n2);
    sort(n2); // podgotovka Uslovie 2
   izhod(n2);      // za vsichki koli - Uslovie 2
  filter(n2);// podgotovka na Uslovie 3 - masiv SF
  sort_klas();//podgotovka na Uslovie 3 - podrezhda masiva SF po klas i data na vryshtane
izhod2();// spisyk na koli - Uslovie 3   
sr2=suma(n2)/n2;
cout<<"\n\nSrednata stojnost na kolite e = "<<sr2<<" leva.";

 cout<<"\n------------------------------";
 cout<<"\nTRETA FIRMA:\n";
cout<<"------------------------------";
//cin.ignore();
    vhod(n3);
    sort(n3); // podgotovka Uslovie 2
   izhod(n3);      // za vsichki koli - Uslovie 2
  filter(n3);// podgotovka na Uslovie 3 - masiv SF
  sort_klas();//podgotovka na Uslovie 3 - podrezhda masiva SF po klas i data na vryshtane
izhod2();// spisyk na koli - Uslovie 3   
sr3=suma(n3)/n3;
cout<<"\n\nSrednata stojnost na kolite e = "<<sr3<<" leva.";
// Naj-malka ot trite sredni ceni
if ((sr1<=sr2)&&(sr1<=sr3))
cout<<"\n\nNaj-malkata sredna stojnost e "<<sr1<<" leva.";
else 
if(sr2<=sr3) cout<<"\n\nNaj-malkata sredna stojnost e "<<sr2<<" leva.";
else cout<<"\n\nNaj-malkata sredna stojnost e "<<sr3<<" leva.";
cout<<"\n"; 
system("pause");

return 0;
}
