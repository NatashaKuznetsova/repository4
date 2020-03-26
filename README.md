# repository4
type
 PItem=^TItem;
 TItem=record
   n:string;
   l,r:PItem;
 end;

 procedure Add( Var Tree:PItem; x:string);
 begin
   if Tree = nil then
   begin
     New(Tree);
     Tree^.n:=x;
     Tree^.l:= nil;
     Tree^.r:= nil;
   end
   else
   if Tree^.n < x then
   Add(Tree^.r, x)
   else
   Add(Tree^.l, x);
 end;

 Procedure Print( Tree:PItem; h:integer);
  begin
    if Tree<> nil then
    begin
      Print(Tree^.r, h+2);
      writeln(Tree^.n: h);
      Print(Tree^.l, h+2);
 end;
    end;


      procedure DeleteTree ( var Tree: PItem);
      begin
        if Tree <> nil then
        begin

        DeleteTree(Tree^.r);
        DeleteTree(Tree^.l);
        Dispose (Tree);
        Tree:=nil;
        end;
      end;

var
  tree: PItem = nil;
  s: string;
  f: TextFile;
begin
  AssignFile(f, 'C:\Users\Kuzne\Desktop\gf.txt');
  Reset(f);
  while not Eof(f) do
  begin
    Readln(f, s);
    Add(tree, s);
  end;
  CloseFile(f);
  writeln('Дерево: ');
  Print(Tree, 2);
  DeleteTree(Tree);


   Read;
end.  
