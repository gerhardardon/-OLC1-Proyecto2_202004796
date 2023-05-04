# -OLC1-Proyecto2_202004796

S
  : INSTRUCCIONES EOF
;


INSTRUCCIONES
  : INSTRUCCIONES INSTRUCCION  
  | INSTRUCCION                
;
/*----- Todo bien Hasta aca */
INSTRUCCION
  : DECLARACION_VARIABLE 
  | DECLARACION_FUNCION 
  | DECLARACION_TYPE 
  | ASIGNACION 
  | PUSH_ARREGLO 
  | ARRAY_POP
  | POP_ARREGLO 
  | CONSOLE_LOG 
  | PRINT 
  | PRINTLN 
  | INSTRUCCION_IF 
  | SWITCH 
  | BREAK 
  | RETURN 
  | CONTINUE 
  | WHILE 
  | DO_WHILE 
  | DO_UNTIL 
  | FOR 
  | FOR_OF 
  | FOR_IN 
  | GRAFICAR_TS 
  | LLAMADA_FUNCION 
  | INCREMENTO_DECREMENTO 
  | FUNCION_NATIVA 
;

LLAMADA_FUNCION 
  : id par_izq par_der punto_coma
  | id par_izq LISTA_EXPRESIONES par_der punto_coma 
;

LLAMADA_FUNCION_EXP 
  : id par_izq par_der 
  | id par_izq LISTA_EXPRESIONES par_der 
;
FUNCION_NATIVA 
  : TYPE_OF 
  | TO_STRING 
  | TO_CHARARRAY 
  | TO_UPPER 
  | TO_LOWER 
  | ROUND 
  | LENGTH 
  | RUN 
;
TYPE_OF 
  : typeof par_izq Lista_EXPRESIONES par_der
;
TO_STRING 
  : tostring par_izq LISTA_EXPRESIONES  par_der 
;
TO_CHARARRAY 
  : tochararray par_izq LISTA_EXPRESIONES par_der
;
TO_UPPER 
  : toupper par_izq LISTA_EXPRESIONES par_der
;
TO_LOWER
  : tolower par_izq LISTA_EXPRESIONES par_der
;
ROUND 
  : round par_izq LISTA_EXPRESIONES par_der
;
LENGTH 
  : length par_izq LISTA_EXPRESIONES par_der
;
RUN
  : run LLAMADA_FUNCION
;

GRAFICAR_TS 
  : graficar_ts par_izq par_der punto_coma 
;

WHILE 
  : while par_izq EXP par_der llave_izq INSTRUCCIONES llave_der 
  ;

DO_WHILE 
  : do llave_izq INSTRUCCIONES llave_der while par_izq EXP par_der punto_coma 
;
DO_UNTIL 
  : do llave_izq INSTRUCCIONES llave_der until par_izq EXP par_der punto_coma 
  ;

FOR 
  : for par_izq DECLARACION_VARIABLE EXP punto_coma EXP  par_der llave_izq INSTRUCCIONES llave_der
  | for par_izq ASIGNACION EXP punto_coma EXP par_der llave_izq INSTRUCCIONES llave_der 
  ;

FOR_OF 
  : for par_izq TIPO_DEC_VARIABLE id of EXP par_der llave_izq INSTRUCCIONES llave_der 
  ;

FOR_IN 
  : for par_izq TIPO_DEC_VARIABLE id in EXP par_der llave_izq INSTRUCCIONES llave_der 
  ;

ASIGNACION 
  : id TIPO_IGUAL EXP punto_coma 
  | id LISTA_ACCESOS_TYPE TIPO_IGUAL EXP punto_coma 
  | ACCESO_ARREGLO TIPO_IGUAL EXP punto_coma 
;

TIPO_IGUAL 
  : igual 
  | mas igual 
  | menos igual 
;

ASIGNACION_FOR 
  : id TIPO_IGUAL EXP 
  | id mas_mas 
  | id menos_menos 
  | id EXP 
;

SWITCH 
  : switch par_izq EXP par_der llave_izq LISTA_CASE llave_der 
  

LISTA_CASE 
  : LISTA_CASE CASE 
  | CASE 
  | DEFAULT 
  | LISTA_CASE DEFAULT 
;

CASE 
  : case EXP dos_puntos INSTRUCCIONES 
;

DEFAULT 
  : default dos_puntos INSTRUCCIONES 
;

CONTINUE 
  : continue punto_coma 
;

BREAK 
  : break punto_coma 
;

RETURN 
  : return EXP punto_coma 
  | return punto_coma 
;

INSTRUCCION_IF 
  : IF 
  | IF ELSE 
  | IF LISTA_ELSE_IF  
  | IF LISTA_ELSE_IF ELSE  
;

IF 
  : if par_izq EXP par_der llave_izq INSTRUCCIONES llave_der 
;

ELSE 
  : else llave_izq INSTRUCCIONES llave_der 
;

ELSE_IF 
  : elif par_izq EXP par_der llave_izq INSTRUCCIONES llave_der 
;

LISTA_ELSE_IF 
  : LISTA_ELSE_IF ELSE_IF  
  | ELSE_IF "" 
;

PUSH_ARREGLO 
  : id punto push par_izq EXP par_der punto_coma  
  | id LISTA_ACCESOS_TYPE punto push par_izq EXP par_der punto_coma  
;
POP_ARREGLO 
  : ARRAY_POP punto_coma  


DECLARACION_FUNCION 
  //Funcion sin parametros y con tipo -> function test() : TIPO 
  
  :TIPO_VARIABLE_NATIVA id par_izq par_der llave_izq INSTRUCCIONES llave_der 

  //Funcion con parametros y con tipo -> function test ( LISTA_PARAMETROS ) : TIPO 
  
  | TIPO_VARIABLE_NATIVA id par_izq LISTA_PARAMETROS par_der llave_izq INSTRUCCIONES llave_der 
;

LISTA_PARAMETROS 
  : LISTA_PARAMETROS coma PARAMETRO  //Revisar si agrego o no coma
  | PARAMETRO 
;

PARAMETRO 
  : int id 
  | string id 
  | boolean id 
  | double id 
  | char id 
;

DECLARACION_TYPE 
  : type id igual llave_izq LISTA_ATRIBUTOS llave_der 
  | type id igual llave_izq LISTA_ATRIBUTOS llave_der punto_coma 
;

LISTA_ATRIBUTOS /*-->TR -- EJ<--*/
  : ATRIBUTO coma LISTA_ATRIBUTOS  //Revisar si agrego o no coma
  | ATRIBUTO 
;

ATRIBUTO 
  : id dos_puntos TIPO_VARIABLE_NATIVA 
  | id dos_puntos TIPO_VARIABLE_NATIVA LISTA_CORCHETES 
;

DECLARACION_VARIABLE 
  : TIPO_VARIABLE_NATIVA LISTA_DECLARACIONES punto_coma 
;

//TODO: REVISAR DEC_ID_COR Y DEC_ID_COR_EXP
LISTA_DECLARACIONES 
  : LISTA_DECLARACIONES coma DEC_ID   //No utilice las comas
  | LISTA_DECLARACIONES coma DEC_ID_TIPO  
  | LISTA_DECLARACIONES coma DEC_ID_TIPO_CORCHETES  
  | LISTA_DECLARACIONES coma DEC_ID_EXP  
  | LISTA_DECLARACIONES coma DEC_ID_TIPO_EXP  
  | LISTA_DECLARACIONES coma DEC_ID_TIPO_CORCHETES_EXP  
  | DEC_ID  
  | DEC_ID_TIPO  
  | DEC_ID_TIPO_CORCHETES  
  | DEC_ID_EXP  
  | DEC_ID_TIPO_EXP  
  | DEC_ID_TIPO_CORCHETES_EXP  
;

//let id : TIPO_VARIABLE_NATIVA LISTA_CORCHETES = EXP ;
DEC_ID_TIPO_CORCHETES_EXP 
  : id dos_puntos TIPO_VARIABLE_NATIVA LISTA_CORCHETES igual EXP 
;

//let id : TIPO_VARIABLE_NATIVA = EXP;
DEC_ID_TIPO_EXP 
  : id dos_puntos TIPO_VARIABLE_NATIVA igual EXP 
;

// id = EXP ;
DEC_ID_EXP 
  : id igual EXP 
;

// id : TIPO_VARIABLE_NATIVA ;
DEC_ID_TIPO  
  : id dos_puntos TIPO_VARIABLE_NATIVA 
;

//let id ;
DEC_ID  
  : id  
;

//let id : TIPO_VARIABLE_NATIVA LISTA_CORCHETES ;
DEC_ID_TIPO_CORCHETES 
  : id dos_puntos TIPO_VARIABLE_NATIVA LISTA_CORCHETES 
;

LISTA_CORCHETES 
  : LISTA_CORCHETES cor_izq cor_der 
  | cor_izq cor_der 
;

INCREMENTO_DECREMENTO
  : id mas_mas punto_coma 
  | id menos_menos punto_coma 
  | menos_menos id punto_coma 
  | mas_mas id punto_coma 
;

EXP
  //Operaciones Aritmeticas
  : menos EXP %prec umenos  
  | EXP mas EXP  
  | EXP menos EXP  
  | EXP por EXP  
  | EXP div EXP  
  | EXP mod EXP  
  | EXP potencia EXP  
  | id mas_mas  
  | id menos_menos /*-->TR- EJ<--*/ 
  | par_izq EXP par_der  
  //Operaciones de Comparacion
  | EXP mayor EXP  
  | EXP menor EXP  
  | EXP mayor_igual EXP  
  | EXP menor_igual EXP  
  | EXP igual_que EXP  
  | EXP dif_que EXP  
  //Operaciones Lógicas
  | EXP and EXP  
  | EXP or EXP  
  | not EXP  
  | casteo EXP  
  | tolower par_izq EXP par_der  
  | toupper par_izq EXP par_der   
  | round par_izq EXP par_der   
  | length par_izq EXP par_der   
  | typeof par_izq EXP par_der   
  | tostring  par_izq EXP par_der   
  | tochararray  par_izq EXP par_der   
  //Valores Primitivos
  | number  
  | string  
  | char  
  | double  
  | int  
  | id   
  | true  
  | false  
  | null  
  //Arreglos
  | cor_izq LISTA_EXPRESIONES cor_der  
  | cor_izq cor_der  
  | ACCESO_ARREGLO  
  | ARRAY_LENGTH  
  | ARRAY_POP  
  //Types - accesos
  | ACCESO_TYPE  
  | TYPE  
  //Ternario
  | TERNARIO  
  //Funciones
  | LLAMADA_FUNCION_EXP  
;

CASTEO 
  : TIPO_VARIABLE_NATIVA par_izq LISTA_EXPRESIONES par_der 
;

TYPE 
  : llave_izq ATRIBUTOS_TYPE llave_der 
;

ATRIBUTOS_TYPE 
  : ATRIBUTO_TYPE coma ATRIBUTOS_TYPE 
  | ATRIBUTO_TYPE 
;

ATRIBUTO_TYPE 
  : id dos_puntos EXP 
;

ARRAY_LENGTH 
  : id punto length  
  | id LISTA_ACCESOS_ARREGLO punto length  
  | id LISTA_ACCESOS_TYPE punto length  
;

ARRAY_POP 
  : id punto pop par_izq par_der punto_coma 
  | id LISTA_ACCESOS_ARREGLO punto pop par_izq par_der  
  | id LISTA_ACCESOS_TYPE punto pop par_izq par_der   
;

TERNARIO 
  : EXP interrogacion EXP dos_puntos EXP 
;

ACCESO_ARREGLO 
  : id LISTA_ACCESOS_ARREGLO 
;

ACCESO_TYPE 
  : id LISTA_ACCESOS_TYPE 
;

LISTA_ACCESOS_TYPE 
  : LISTA_ACCESOS_TYPE punto id 
  | punto id 
  | LISTA_ACCESOS_TYPE punto id LISTA_ACCESOS_ARREGLO 
  | punto id LISTA_ACCESOS_ARREGLO 
;

LISTA_ACCESOS_ARREGLO 
  : LISTA_ACCESOS_ARREGLO cor_izq EXP cor_der 
  | cor_izq EXP cor_der 
;

LISTA_EXPRESIONES 
  : LISTA_EXPRESIONES coma EXP 
  | EXP 
;

/*TR - EJ*/


/*TR - EJ*/
TIPO_VARIABLE_NATIVA
  : char    
  | string  
  | boolean 
  | double  
  | int     
  | void    
  | id      
;

CONSOLE_LOG 
  : console punto log par_izq LISTA_EXPRESIONES par_der punto_coma 
;

PRINT 
  : print par_izq EXP par_der punto_coma 
;
PRINTLN 
  : println par_izq EXP par_der punto_coma 
;
