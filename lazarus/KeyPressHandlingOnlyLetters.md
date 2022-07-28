# Key pressed, characters sent (KeyPress)


To handle OnKeyPress Events for Unicode characters you will need to call **OnUTF8KeyPress** event instead of **OnKeyPress**

1. You need to add **Character** to use _IsLetter_ function 
2. Add an _OnUTF8KeyPress_ to TEdit
3. Convert _UTF8Key_ to String, so you can use _IsLetter_ function

if needed you can add conditions for space (' '), enter (#13), backspace (#8) and delete key (#7)

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

Source: https://wiki.lazarus.freepascal.org/LCL_Key_Handling
