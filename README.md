%Esta función me permite resolver un sistema lineal Ax=b, y
%hallar su solución por el método de eliminación gaussiana y 
%sustitución hacia atrás, usando una matríz aumentada [A|b].

function[A]=backreplace(archivodatos)

%Esta función asigna a la variable matriz el archivo de 
%datos externo y le indica que es de solo lectura.

matriz=fopen('archivodatos.txt','r');

%Se declaran dos variables que contienen el número de
%filas y el número de columnas de la matriz Ax=b.

nf=fscanf(matriz,'%d',1);
nc=fscanf(matriz,'%d',1);

%Aquí Inicializamos con "0s" la matriz Aumentada [A|b] y 
%cargamos los valores de los coeficientes de la matriz A.

A=zeros(nf,nc+1);
for i=1:1:nf
    for j=1:1:nc
        A(i,j)=fscanf(matriz,'%d',1);
    end
end

%En esta instrucción cargamos los datos del vector a la 
%matriz aumentada [A|b].

k=nc+1;
for y=1:1:nf
    A(y,k)=fscanf(matriz,'%d',1);
end

%Aquí evaluamos si algún elemento de la diagonal ppal de la 
%Matriz A es igual a cero.

for i=1:1:nc
    if A(i,i)==0
       disp('ATENCION: La Matríz no puede tener "0s en la diagonal ppal')
       return
    end
end        

%Aquí Inicializamos con "0s" el vector c que nos va a ser-
%vir para cargar los valores de la variables x que hallemos.

x=zeros(nf,1);
disp('El Orden de la matríz de coeficientes A es: ')
disp(nf)
disp('La Matríz Aumentada [A|b] es: ')
disp(A)
n=nf;

%Estas subrutinas hacen "1s" las entradas de la diagonal
%principal de la matriz A.

for i=1:1:n
    for j=1:1:n+1
        B(i,j)=(A(i,j)/A(i,i));
    end

%Estas Subrutinas hacen "0s" las entradas debajo de la 
%diagonal principal de la Matriz A.

    for k=i+1:1:n
        for z=1:1:n+1
            B(k,z)=A(k,z)-(B(i,z)*A(k,i));
        end
    end
    A=B;
end

%Estas Subrutinas calculan los valores de las incógnitas
%del sistema lineal Ax=b y lo cargan al vector x.

x(n,1)=(A(i,n+1)/A(n,n));
for y=n-1:-1:1
    s=0;
    for m=y+1:n
        s=s+(A(y,m)*x(m,1));
    end
    x(y,1)=(A(y,n+1)-s)/A(y,y);
end

%En estas Subrutinas se muestra el vector x en pantalla,
%ordenado en forma ascendente desde x1 hasta xn.

disp('El vector x=[x1,x2,...,xn], ordenado en forma')
disp('ascendente desde x1(arriba) hasta xn(abajo) es: ,')
for p=1:1:n
    disp('x:')
    disp(x(p))
end    
disp('La Matríz Aumentada [B|d] Reducida y escalonada por filas es:')
return
