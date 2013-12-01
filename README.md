laba613
=======
//---------------------------------------------------------------------------
#include <iostream.h>
#include <string.h>
#include <vcl.h>
#pragma hdrstop
#include "Unit1.h"
#include <wchar.h>
//---------------------------------------------------------------------------
#pragma package(smart_init)
#pragma resource "*.dfm"
TForm1 *Form1;
int n=0;
class ZP
{ 	public:
	UnicodeString ima;
	UnicodeString dt;
	int num;
};
ZP Knig[40];


//---------------------------------------------------------------------------
__fastcall TForm1::TForm1(TComponent* Owner)
	: TForm(Owner)
{

}
//---------------------------------------------------------------------------



void __fastcall TForm1::Button1Click(TObject *Sender)
{	if (Edit1->Text.IsEmpty() || Edit2->Text.IsEmpty() || Edit3->Text.IsEmpty() )
{	  ShowMessage("Одно из полей ввода не содержит информации");}
else
{	Knig[n].ima=Edit1->Text;
	Knig[n].dt=Edit2->Text;
	Knig[n].num=StrToInt(Edit3->Text);
	n++;
	Button2->Click();
}
}
//---------------------------------------------------------------------------



void __fastcall TForm1::Button2Click(TObject *Sender)
{   StringGrid1->RowCount=n+1;
	StringGrid1->ColCount=4;
	StringGrid1->Cells[1][0]="Фамилия";
	StringGrid1->Cells[2][0]="Дата";
	StringGrid1->Cells[3][0]="Телефон";

	for (int i = 0; i < n; i++) {
	StringGrid1->Cells[0][i+1]=i+1;
	StringGrid1->Cells[1][i+1]=Knig[i].ima;
	StringGrid1->Cells[2][i+1]=Knig[i].dt;
	StringGrid1->Cells[3][i+1]=Knig[i].num;
	}

}

//---------------------------------------------------------------------------



void __fastcall TForm1::Button3Click(TObject *Sender)
{
UnicodeString min;
ZP buf;
int minI;
	for (int i = 0; i < n-1; i++)
			{ 	Button2->Click();
				int minI = i;
				for (int j = i + 1; j < n; j++)
				{
					if (wcscmp(Knig[j].ima.c_str(),min.c_str())<0)
					{
						minI = j;
					}
				}
				buf = Knig[i];
				Knig[i] = Knig[minI];
				Knig[minI] = buf;
			}
			}
//---------------------------------------------------------------------------



//---------------------------------------------------------------------------



void __fastcall TForm1::Button4Click(TObject *Sender)
{int nd=StrToInt(Edit4->Text);
 if ( nd > n || nd < 1)
	{
		ShowMessage("Ошибка удаления");

	}
	else{
	for(int i = nd-1; i < n-1; i++)
	{
		Knig[i] = Knig[i + 1];
	}
	n--;
	Button2->Click();
	}

}
//---------------------------------------------------------------------------

void __fastcall TForm1::Button5Click(TObject *Sender)
{int nb=StrToInt(Edit5->Text);
int nbb;
nbb=nb;
 if ( nb > n || nb < 1)
	{
		ShowMessage("Ошибка добавить");

	}
	else{

		if (Edit1->Text.IsEmpty() || Edit2->Text.IsEmpty() || Edit3->Text.IsEmpty() )
 {	  	ShowMessage("Одно из полей ввода не содержит информации");}
		else
		{n++;
		for(int i = n; i > nb-1; i--)
		{
		Knig[i] = Knig[i-1];
		}

		Knig[nb-1].ima=Edit1->Text;
		Knig[nb-1].dt=Edit2->Text;
		Knig[nb-1].num=StrToInt(Edit3->Text);

		}
Button2->Click();
}
}


void __fastcall TForm1::ДатеClick(TObject *Sender)
{
UnicodeString min;
ZP buf;
int pos;
int j,minI;
for (int i = 0; i < n; i++) {
min=Knig[i].dt;
minI=i;
for (int j=i; j<=n; j++) {
if (wcscmp(Knig[j].ima.w_str(),min.w_str())>0){
min=Knig[i].dt;
minI=j;
}
}
buf=Knig[i];
Knig[i]=Knig[minI];
Knig[minI]=buf;
}
}

//---------------------------------------------------------------------------
