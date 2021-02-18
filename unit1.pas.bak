unit Unit1;

{$mode objfpc}{$H+}

interface

uses
  Classes, SysUtils, FileUtil, Forms, Controls, Graphics, Dialogs, StdCtrls,
  ExtCtrls, Buttons, Menus, Spin, DateUtils, MMSystem;

type

  { TForm1 }

  TForm1 = class(TForm)
    Button1: TButton;
    Button2: TButton;
    Button3: TButton;
    Button4: TButton;
    Button5: TButton;
    CheckBox1: TCheckBox;
    CheckBox2: TCheckBox;
    Edit1: TEdit;
    GroupBox1: TGroupBox;
    GroupBox2: TGroupBox;
    GroupBox3: TGroupBox;
    Image1: TImage;
    Image2: TImage;
    Image3: TImage;
    Image4: TImage;
    Label1: TLabel;
    Label2: TLabel;
    Label3: TLabel;
    Label4: TLabel;
    Label5: TLabel;
    Label6: TLabel;
    Labelq: TLabel;
    Labela: TLabel;
    Labelb: TLabel;
    Labelc: TLabel;
    Memo1: TMemo;
    MenuItem1: TMenuItem;
    MenuItem10: TMenuItem;
    MenuItem11: TMenuItem;
    MenuItem13: TMenuItem;
    MenuItem14: TMenuItem;
    MenuItem8: TMenuItem;
    MenuItem2: TMenuItem;
    MenuItem3: TMenuItem;
    MenuItem4: TMenuItem;
    MenuItem5: TMenuItem;
    MenuItem6: TMenuItem;
    MenuItem7: TMenuItem;
    MenuItem12: TMenuItem;
    MenuItem9: TMenuItem;
    OpenDialog1: TOpenDialog;
    PopupMenu1: TPopupMenu;
    PopupMenu2: TPopupMenu;
    PopupMenu3: TPopupMenu;
    PopupMenu4: TPopupMenu;
    SpinEdit1: TSpinEdit;
    Timer1: TTimer;
    Timer2: TTimer;
    procedure Button1Click(Sender: TObject);
    procedure Button2Click(Sender: TObject);
    procedure Button3Click(Sender: TObject);
    procedure Button4Click(Sender: TObject);
    procedure Button5Click(Sender: TObject);
    procedure CheckBox2Change(Sender: TObject);
    procedure Edit1KeyDown(Sender: TObject; var Key: Word);
    procedure FormCreate(Sender: TObject);
    procedure FormKeyDown(Sender: TObject; var Key: Word);
    procedure Image1Click(Sender: TObject);
    procedure LabelaClick(Sender: TObject);
    procedure LabelbClick(Sender: TObject);
    procedure LabelcClick(Sender: TObject);
    procedure MenuItem10Click(Sender: TObject);
    procedure MenuItem11Click(Sender: TObject);
    procedure MenuItem13Click(Sender: TObject);
    procedure MenuItem14Click(Sender: TObject);
    procedure MenuItem1Click(Sender: TObject);
    procedure MenuItem2Click(Sender: TObject);
    procedure MenuItem3Click(Sender: TObject);
    procedure MenuItem4Click(Sender: TObject);
    procedure MenuItem5Click(Sender: TObject);
    procedure MenuItem6Click(Sender: TObject);
    procedure MenuItem7Click(Sender: TObject);
    procedure MenuItem8Click(Sender: TObject);
    procedure MenuItem9Click(Sender: TObject);
    procedure SpinEdit1Change(Sender: TObject);
    procedure Timer1Timer(Sender: TObject);
    procedure Timer2Timer(Sender: TObject);
    procedure loadQuestion(x: integer);
    procedure loadQuestions(filename: string);
    function checkQuestion(nr: integer; t: integer): integer;
  private
    { private declarations }
  public
    { public declarations }
  end;

var
  Form1: TForm1;
  Date: TDateTime;
  days, weeks, months, years: integer;
  day1, day2, month1, month2, year2, year1, photo: integer;
  d, m, y: word;
  content: array of array of string;
  quest: array [0..9] of integer;
  pos, score, total, id: integer;
  question, en: boolean;
  questions: integer;
  sub:textfile;
  path: string;

implementation

{$R *.lfm}

{ TForm1 }
                                                 //TO-DO (include in 3.5 release)
procedure TForm1.Timer1Timer(Sender: TObject);   //minigame design ???
begin                                            //new functions maybe
  Date:= EncodeDate(2021, 7, 10);
  DecodeDate(Now, y, m, d);
  day1:= d;
  month1:= m;
  year1:= y;
  DecodeDate(Date, y, m, d);
  day2:= d;
  month2:= m;
  year2:= y;
  //label3.caption:= inttostr(day2) + '.' + inttostr(month2) + '.' + inttostr(year2);
  if day2 < day1 then
  begin
       if month2 = 3 then
       begin
            if IsInLeapYear(Date) then
            begin
                day2 += 29;
            end
            else day2 += 28;
        end

        else if ((month2 = 5) or (month2 = 7) or (month2 = 10) or (month2 = 12)) then
        begin
           day2 += 30;
        end
        else day2 += 31;

        month2 := month2 - 1;
  end;

    if month2 < month1 then
    begin
        month2 += 12;
        year2 -= 1;
    end;

    days := day2 - day1;
    months := month2 - month1;
    years := year2 - year1;
    weeks := days div 7;
    days -= weeks*7;
  label2.caption:= inttostr(years) + ' years, ' + inttostr(months) + ' months, ' + inttostr(weeks) + ' weeks, ' + inttostr(days) + ' days';

end;

procedure TForm1.Timer2Timer(Sender: TObject);
begin
  photo+= 1;
  if FileExists(path + inttostr(photo) + '.jpg') then
  begin
       image1.Picture.LoadFromFile(path + inttostr(photo)+'.jpg');
  end
  else
  begin
      if checkbox1.checked = true then
      begin
        photo:= 1;
        image1.Picture.LoadFromFile(path + inttostr(photo) + '.jpg');
      end
      else
      begin
        photo:= 1;
        timer2.enabled:= false;
        image1.Picture.loadfromfile(path + inttostr(photo)+'.jpg');
        menuitem4.caption:= 'Slideshow';
      end;
  end;
  timer2.interval:= spinedit1.value * 1000;
end;

procedure TForm1.Image1Click(Sender: TObject);
begin
   photo+= 1;
   if FileExists(path + inttostr(photo) + '.jpg') then
   begin
        image1.Picture.LoadFromFile(path + inttostr(photo)+'.jpg');
   end
   else
   begin
       photo:= 1;
       if FileExists(path + inttostr(photo) + '.jpg') then image1.Picture.LoadFromFile(path + inttostr(photo) + '.jpg')
       else showMessage('Slideshow pictures not found, make sure they are in the right folder.');
   end;
end;

procedure TForm1.LabelaClick(Sender: TObject);
begin
  if question = false then
  begin
    question:= true;
    if strtoint(content[pos, 4]) = 1 then
    begin
      labela.font.color:= clGreen;
      score += 1;
    end
    else
      labela.font.color:= clRed;
    button4.visible:= true;
    if strtoint(content[pos, 4]) = 2 then labelb.font.color:= clGreen;
    if strtoint(content[pos, 4]) = 3 then labelc.font.color:= clGreen;
  end;
end;

procedure TForm1.LabelbClick(Sender: TObject);
begin
  if question = false then
  begin
    question:= true;
    if strtoint(content[pos, 4]) = 2 then
    begin
      labelb.font.color:= clGreen;
      score += 1;
    end
    else
      labelb.font.color:= clRed;
    button4.visible:= true;
    if strtoint(content[pos, 4]) = 1 then labela.font.color:= clGreen;
    if strtoint(content[pos, 4]) = 3 then labelc.font.color:= clGreen;
  end;
end;

procedure TForm1.LabelcClick(Sender: TObject);
begin
  if question = false then
  begin
    question:= true;
    if strtoint(content[pos, 4]) = 3 then
    begin
      labelc.font.color:= clGreen;
      score += 1;
    end
    else
      labelc.font.color:= clRed;
    button4.visible:= true;
    if strtoint(content[pos, 4]) = 1 then labela.font.color:= clGreen;
    if strtoint(content[pos, 4]) = 2 then labelb.font.color:= clGreen;
  end;
end;

procedure TForm1.MenuItem10Click(Sender: TObject);
begin
  score:= 0;
  setlength(content,0);
  if FileExists(path + 'questions.txt') then
  begin
     loadQuestions(path + 'questions.txt');
     //label1.caption:= label1.caption + id;
     labelq.caption:= 'Are you ready?';
     labela.caption:= 'Total questions loaded: ' + inttostr(questions);
     labelb.caption:= 'Click start to begin';
     labelc.caption:= '';
     labelq.font.color:= clBlack;
     showmessage('Questions reload successfull!');
  end
  else
  begin
    questions:= 0;
    labelq.font.color:= clRed;
    labelq.Caption:= 'Questions not loaded, check if the file exists.';
    labela.caption:= 'File questions.txt is not present in the program directory.';
    labelb.caption:= 'Put file into the same folder as program and try again.';
    labelc.caption:= ''; //space for some info message
    sysutils.beep();
    showmessage('Failed to open file questions.txt!');
  end;
end;

procedure TForm1.MenuItem11Click(Sender: TObject);   //fullscreen option
begin
  if en = false then
  begin
    form1.windowstate:= wsFullScreen;
    form1.borderstyle:= bsNone;
    en:= true;
    image1.Width:= form1.width;
    image1.Height:= form1.height;
    image4.Width:= form1.width;
    image4.Height:= form1.height;
    groupbox1.top:= form1.height - 142;
    groupbox2.top:= form1.height - 254;
    groupbox2.left:= form1.width - 380;
    groupbox3.left:= 25;
    menuitem11.caption:= 'Exit fullscreen';
  end
  else
  begin
    form1.windowstate:= wsNormal;
    form1.borderstyle:= bsSingle;
    form1.height:= 742;
    form1.width:= 1316;
    form1.top:= 131;
    form1.left:= 293;
    groupbox1.top:= 600;
    groupbox2.top:= 488;
    groupbox2.left:= 936;
    groupbox3.left:= 384;
    image1.Width:= form1.width;
    image1.Height:= form1.height;
    image4.Width:= form1.width;
    image4.Height:= form1.height;
    en:= false;
    menuitem11.caption:= 'Fullscreen';
  end;
end;

procedure TForm1.MenuItem13Click(Sender: TObject);
begin
  showmessage('There should be something new in next release ;)');
end;

procedure TForm1.MenuItem14Click(Sender: TObject);
begin
  mciSendString(PChar('stop sound'), nil, 0, 0);
  mciSendString(PChar('stop mp3'), nil, 0, 0);
end;

procedure TForm1.FormCreate(Sender: TObject);
var
  sText: string;
  iLength: integer;
begin
  //path:= 'C:\Program Files\Countdown\';      //directory where all files(photos, music, ...) are stored
  path:= '';           //local files only
  //menuitem9.checked:= false;
  id := -1;
  score:= 0;
  if FileExists(path + 'questions.txt') then
  begin
     loadQuestions(path + 'questions.txt');
     //label1.caption:= label1.caption + id;
     labelq.caption:= 'Are you ready?';
     labela.caption:= 'Total questions loaded: ' + inttostr(questions);
     labelb.caption:= 'Click start to begin';
     labelc.caption:= '';
  end
  else
  begin
    questions:= 0;
    labelq.font.color:= clRed;
    labelq.Caption:= 'Questions not loaded, check if the file exists.';
    labela.caption:= 'File questions.txt is not present in the program directory.';
    labelb.caption:= 'Put file into the same folder as program and try again.';
    labelc.caption:= ''; //space for some info message
  end;
  sText := Memo1.Lines.Text;
  while 1 = 1 do
  begin
    iLength := Length(sText);
    if (Ord(sText[iLength-1])=13) and (Ord(sText[iLength])=10) then
      Delete(sText, iLength-1, 2)
    else Break;
  end;
  Memo1.Lines.Text := sText;
  if id > -1 then
  begin
    if FileExists(path + inttostr(id) + '.jpg') then image1.picture.LoadFromFile(path + inttostr(id) + '.jpg');
    photo:= id;
  end
  else photo:= 1;
  en:= false;
end;

procedure TForm1.FormKeyDown(Sender: TObject; var Key: Word);
begin
  //showmessage(inttostr(Key));
  if Key = 27 then
  begin
    form1.windowstate:= wsNormal;
    form1.borderstyle:= bsSingle;
    form1.height:= 742;
    form1.width:= 1316;
    form1.top:= 131;
    form1.left:= 293;
    groupbox1.top:= 600;
    groupbox2.top:= 488;
    groupbox2.left:= 936;
    groupbox3.left:= 384;
    image1.Width:= form1.width;
    image1.Height:= form1.height;
    image4.Width:= form1.width;
    image4.Height:= form1.height;
    en:= false;
    menuitem11.caption:= 'Fullscreen';
  end
  else if Key = 70 then
  begin
    form1.windowstate:= wsFullScreen;
    form1.borderstyle:= bsNone;
    en:= true;
    image1.Width:= form1.width;
    image1.Height:= form1.height;
    image4.Width:= form1.width;
    image4.Height:= form1.height;
    groupbox1.top:= form1.height - 142;
    groupbox2.top:= form1.height - 254;
    groupbox2.left:= form1.width - 380;
    groupbox3.left:= 25;
    menuitem11.caption:= 'Exit fullscreen';
  end
  else if Key = 192 then
  begin
    if edit1.visible = false then
    begin
      edit1.visible:= true;
      edit1.enabled:= true;
      edit1.text:= '';
    end
    else
    begin
      edit1.visible:= false;
      edit1.enabled:= false;
    end;
  end;
end;

procedure TForm1.Button1Click(Sender: TObject);
begin
  groupbox1.visible:= false;
end;

procedure TForm1.Button2Click(Sender: TObject);
begin
  groupbox2.visible:= false;
end;

procedure TForm1.Button3Click(Sender: TObject);
var
  i: integer;
begin
  for i:= 0 to 9 do quest[i]:= 0;
  if questions > 0 then
  begin
    Randomize;
    pos:= random(questions);
    score:= 0;
    total:= 1;
    quest[total-1]:= pos;
    loadQuestion(pos);
    button3.visible:= false;
    image3.visible:= false;
    image2.visible:= false;
  end
  else
  begin
    sysutils.beep();
    showmessage('No questions loaded, make sure the questions.txt file is present in the right directory.');
  end;
  mciSendString(pchar('stop sound'),nil, 0, 0);
end;

procedure TForm1.Button4Click(Sender: TObject);
begin
  if total < 10 then
  begin
    Randomize;
    pos:= random(questions);         //random question generation
    pos:= checkQuestion(pos, total);
    loadQuestion(pos);
    total += 1;
    quest[total-1]:= pos;
  end
  else
  begin
    labelq.caption:= 'Congratulations!';
    labela.font.color:= clBlack;
    labela.caption:= 'You have ' + inttostr(score) + '/10 points!';
    labelb.caption:= '';
    labelc.caption:= '';
    button3.caption:= 'Start over';
    button3.visible:= true;
    button4.visible:= false;
    //label6.visible:= false;
    if score >= 5 then
    begin
      image2.Visible:= true;
      mciSendString(PChar('stop mp3'), nil, 0, 0);
      mciSendString(PChar('open "' + path + 'Neverending_story.mp3' + '" alias sound'), nil, 0, 0);
      mciSendString(Pchar('play sound from 0'), nil, 0, 0);

    end
    else
      image3.visible:= true;
  end;
end;

procedure TForm1.Button5Click(Sender: TObject);
begin
  groupbox3.visible:= false;
end;

procedure TForm1.CheckBox2Change(Sender: TObject);
begin
  if checkbox2.checked = true then   mciSendString(Pchar('play mp3 repeat'), nil, 0, 0)
  else mciSendString(Pchar('play mp3'), nil, 0, 0);
end;

procedure TForm1.Edit1KeyDown(Sender: TObject; var Key: Word);
var
  command: string;
  nr: integer;
begin
  //showmessage('key pressed: ' + inttostr(Key));
  if Key = 13 then
  begin
    command := copy(edit1.text, 1, 3);
    case (lowercase(command)) of
     'img': begin
             nr := photo;
             if copy(edit1.text, 4, 5) = '' then showmessage('Current picture number is ' + inttostr(photo) + '.') else
             photo:= strtoint(trim(copy(edit1.text, 4, 5)));
             if FileExists(path + inttostr(photo) + '.jpg') then image1.Picture.LoadFromFile(path + inttostr(photo) + '.jpg')
             else begin
               showMessage('Picture file not found in current directory!');
               photo:= nr;
             end;
            end;
     'que': begin
              if copy(edit1.text, 4, 5) = '' then
              begin
                groupbox3.visible:= true;
              end
              else
              begin
                loadQuestion(strtoint(trim(copy(edit1.text, 4, 5))) - 1);
                pos:= strtoint(trim(copy(edit1.text, 4, 5))) - 1;
              end;
            end;
     'stp': begin
             mciSendString(PChar('stop sound'), nil, 0, 0);
             mciSendString(PChar('stop mp3'), nil, 0, 0);
            end;
     'tem': begin
             mciSendString(PChar('stop sound'), nil, 0, 0);
             mciSendString(PChar('open "' + path + 'Stranger_Things_theme.mp3' + '" alias mp3'), nil, 0, 0);
             mciSendString(Pchar('play mp3 from 0'), nil, 0, 0);
            end;
     'nes': begin
             mciSendString(PChar('stop mp3'), nil, 0, 0);
             mciSendString(PChar('open "' + path + 'Neverending_story.mp3' + '" alias sound'), nil, 0, 0);
             mciSendString(Pchar('play sound from 0'), nil, 0, 0);
            end;
     'hlp': showmessage('Console commands:'#13#10'img [nr] - displays image given as parameter'#13#10'que [nr] - displays question given as parameter'#13#10'que - opens quiz'#13#10'stp - stops all music'#13#10'tem - plays theme song'#13#10'nes - plays quiz winning song');
    end;
    //edit1.text:= ''; //clear edit after entering command
  end
  else if Key = 192 then
  begin
    edit1.visible:= false;
    edit1.enabled:= false;
  end;
end;

procedure TForm1.MenuItem1Click(Sender: TObject);
begin
  image1.visible:= false;
  image4.visible:= true;
  label1.visible:= false;
  label2.visible:= false;
end;

procedure TForm1.MenuItem2Click(Sender: TObject);
begin
  image4.visible:= false;
  image1.visible:= true;
  label1.visible:= true;
  label2.visible:= true;
end;

procedure TForm1.MenuItem3Click(Sender: TObject);
var
  filename:string;
begin
  if OpenDialog1.Execute then
  begin
      filename:= OpenDialog1.Filename;
      Image1.Picture.LoadFromFile(filename);
  end;
  photo:= 0;
end;

procedure TForm1.MenuItem4Click(Sender: TObject);
begin
  if FileExists(path + '1.jpg') then
  begin
    if timer2.enabled = false then
    begin
      timer2.Enabled:= true;
      menuitem4.caption:= 'Stop shideshow';
    end
    else
    begin
       timer2.enabled:= false;
       menuitem4.caption:= 'Slideshow';
    end;
  end
  else showMessage('Slideshow pictures not found, make sure they are in the right folder.');
end;

procedure TForm1.MenuItem5Click(Sender: TObject);
begin
  groupbox1.visible:= true;
end;

procedure TForm1.MenuItem6Click(Sender: TObject);   //play theme procedure
begin
  mciSendString(PChar('stop sound'), nil, 0, 0);
  //sndPlaySound(pchar('Stranger_Things_theme.wav'), snd_Async or snd_NoDefault);
  mciSendString(PChar('open "' + path + 'Stranger_Things_theme.mp3' + '" alias mp3'), nil, 0, 0);
  mciSendString(Pchar('play mp3 from 0'), nil, 0, 0);
  if checkbox2.checked = true then   mciSendString(Pchar('play mp3 repeat'), nil, 0, 0)
end;

procedure TForm1.MenuItem7Click(Sender: TObject);
begin
  groupbox2.visible:= true;
end;

procedure TForm1.MenuItem8Click(Sender: TObject);
begin
  groupbox3.visible:= true;
end;

procedure TForm1.MenuItem9Click(Sender: TObject);   //hidden option for placing files
begin
  close;
  //if menuitem9.checked = false then
  //begin
  //  path:= '';
  //  menuitem9.checked:= true;
  //end
  //else
  //begin
  //  path:= 'C:\Program Files\Countdown\';
  //  menuitem9.checked:= false;
  //end;
end;

procedure TForm1.SpinEdit1Change(Sender: TObject);
begin
  timer2.interval:= spinedit1.value * 1000;
end;

procedure TForm1.loadQuestion(x: integer);
begin
  button4.visible:= false;
  labelq.caption:= inttostr(x + 1) + '. ' + content[x, 0];
  labela.caption:= content[x, 1];
  labelb.caption:= content[x, 2];
  labelc.caption:= content[x, 3];
  labelq.font.color:= clBlack;
  labela.font.color:= clBlack;
  labelb.font.color:= clBlack;
  labelc.font.color:= clBlack;
  question:= false;
  label6.caption:= 'Score: ' + inttostr(score);
end;

procedure TForm1.loadQuestions(filename: string);
var
  lin: string;
  i, j, k: integer;
  zn: char;
begin
  k:= 0;
  i:= 0;
  assignFile(sub, filename);
  reset(sub);
  setlength(content, 1, 5);
  readln(sub, lin);
   Try
    id := strtoint(lin); //if there is no number raise error and do except part
  except
    On E : EConvertError do
    id := 0;             //set id to 0, if conversion error occured
  end;
  if id = 0 then
  begin
    for j:= 1 to length(lin) do
      begin
        zn:= lin[j];
        if ord(zn) = 59 then
           k += 1
        else
          content[i,k]+= zn;
      end;
      k:= 0;
      i += 1;
      setlength(content, i+1, 5);
  end;
  Repeat
      Readln(sub,lin);
      for j:= 1 to length(lin) do
      begin
        zn:= lin[j];
        if ord(zn) = 59 then
           k += 1
        else
          content[i,k]+= zn;
      end;
      k:= 0;
      i += 1;
      setlength(content, i+1, 5);
  Until Eof(sub);
  CloseFile(sub);
  questions:= i;
end;

function TForm1.checkQuestion(nr: integer; t: integer): integer;
var
  i, x:integer;
begin
  Randomize;
  x:= nr;
  for i:= 0 to t do
  begin
    if nr = quest[i] then nr:= random(questions div 2) + random(questions div 2);
  end;
  x:= nr;
  checkQuestion:= x;
end;

end.

