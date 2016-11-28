# prime
program atkin;
var is_prime:array[1..1000001] of boolean; jj:int64;
procedure dosieve(limit:int64);
var i,k,x,y:int64; n:int64;
begin
  for i:=5 to limit do
    is_prime[i]:=false;
  for x:=1 to trunc(sqrt(limit)) do
    for y:=1 to trunc(sqrt(limit)) do
    begin
      n:=4*sqr(x)+sqr(y);
      if (n<=limit) and ((n mod 12 = 1) or (n mod 12 = 5)) then
        is_prime[n]:=not is_prime[n];
      n:=n-sqr(x);
      if (n<=limit) and (n mod 12 = 7) then
        is_prime[n]:=not is_prime[n];
      n:=n-2*sqr(y);
      if (x>y) and (n<=limit) and (n mod 12 = 11) then
        is_prime[n]:=not is_prime[n];
    end;
  for i:=5 to trunc(sqrt(limit)) do
  begin
    if is_prime[i] then
    begin
      k:=sqr(i);
      n:=k;
      while n<=limit do
      begin
        is_prime[n]:=false;
        n:=n+k;
      end;
    end;
  end;
  is_prime[2]:=true;
  is_prime[3]:=true;
end;
begin
  dosieve(1000000);
  for jj:=1 to 1000000 do
    if is_prime[jj] then
      writeln(jj);
end.
