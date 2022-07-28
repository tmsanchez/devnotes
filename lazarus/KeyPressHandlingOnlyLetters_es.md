# Manejo del evento on Key Press para Unicode


Para manejar eventos  OnKeyPress para caracteres  Unicode necesitarás llamar a evento  **OnUTF8KeyPress** en lugar de **OnKeyPress**

1. Agregar la unidad **Character** para poder usar la función _IsLetter_  
2. Agregar un evento _OnUTF8KeyPress_ al TEdit
3. Convertir _UTF8Key_ a String para poder usar la función _IsLetter_ 

Si es necesario se pueden agregar condiciones para manejar las teclas de espacio(' '), enter (#13), retroceso (#8) y borrado (#7)

```pascal
uses
  Classes, SysUtils, Forms, Controls, Graphics, Dialogs, StdCtrls, LCLType, Character;

type

  { TForm1 }

  TForm1 = class(TForm)
    Edit1: TEdit;
    procedure Edit1UTF8KeyPress(Sender: TObject; var UTF8Key: TUTF8Char);
  private

  public

  end;

var
  Form1: TForm1;

implementation

{$R *.lfm}

{ TForm1 }


procedure TForm1.Edit1UTF8KeyPress(Sender: TObject; var UTF8Key: TUTF8Char);
var
  caracterTecleado : UnicodeString;
begin
   caracterTecleado := UTF8ToString(UTF8Key);
   if not IsLetter(caracterTecleado,1)
         and (caracterTecleado <> ' ')
         and (caracterTecleado <> #13)
         and (caracterTecleado <> #8)
         and (caracterTecleado <> #7)then
   begin
       UTF8Key := #0;
   end;
end;

end.  

```

![Only letters sample](https://github.com/tmsanchez/devnotes/blob/main/lazarus/only_letters_lazarus.png "Only letters sample")

Fuente: https://wiki.lazarus.freepascal.org/LCL_Key_Handling
