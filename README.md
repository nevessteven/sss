sss
===

from random import random   #Coordenadas def cria_coordenada(l,c):     '''cria_coordenada: linha x coluna -> coordenada     coordenada(l,c) devolve um elemento do tipo coordenada correspondente a posicao (l,c).'''     if isinstance(l and c,int):         if 1&lt;=l&lt;=4 and 1&lt;=c&lt;=4:             return (l,c)         else: raise ValueError('cria_coordenada: argumentos invalidos')     else:         raise ValueError ('cria_coordenada: argumentos invalidos')  def coordenada_linha(crd):     '''coordenada_linha: coordenada -> inteiro     coordenada_linha(crd) devolve a linha da coordenada'''     return crd[0]  def coordenada_coluna(crd):     '''coordenada_coluna: coordenada -> inteiro     coordenada_coluna(crd) devolve a coluna da coordenada'''      return crd[1]   def e_coordenada(arg):     '''e_coordenada: argumento -> logico     e_coordenada(arg) devolve True caso o argumento seja uma coordenada, False caso contrario'''     if isinstance(arg,tuple) and len(arg) == 2:         if isinstance(coordenada_linha(arg) or coordenada_coluna(arg),int):             if (1&lt;=coordenada_linha(arg)&lt;=4) and (1&lt;=coordenada_coluna(arg)&lt;=4):                 return True             else:                 return False         else:              return False     else:         return False      def coordenadas_iguais(c1,c2):     '''coordenadas_iguais: coordenada x coordenada -> logico     coordenadas_iguais(c1,c2) devolve True caso as coordenadas forem iguais, False caso contrario'''     return c1 == c2  # tabuleiro  def cria_tabuleiro():     '''cria_tabuleiro: (vazio) -> tabuleiro     não recebe nada e cria um tabuleiro com 4x4 (linhas*colunas) e a pontuacao'''     table = [[0 for i in range(1,5)] for i in range(4)]     table = table + [0]     return table  def tabuleiro_posicao(t,c):     '''tabuleiro_posicao: tabuleiro x coordenada -> inteiro     recebe um tabuleiro e uma coordenada(que verifica) e devolve o valor dessa coordenada no tabuleiro'''     if e_coordenada(c):         return t[coordenada_linha(c)-1][coordenada_coluna(c)-1]     else:         raise ValueError('tabuleiro_posicao: argumentos invalidos')   def tabuleiro_pontuacao(t):     '''tabuleiro_pontuacao: tabuleiro -> inteiro     recebe um tabuleiro e devolve a sua pontuacao'''     return t[-1]  def tabuleiro_posicoes_vazias(t):     '''tabuleiro_posicoes_vazias: tabuleiro -> lista     recebe um tabuleiro e devolve lista com posicoes vazias(com zero) desse tabuleiro'''     p=[]     if e_tabuleiro(t):         for i in range(1,5):             for j in range(1,5):                 if tabuleiro_posicao(t,cria_coordenada(i,j)) is 0:                     p=p + [cria_coordenada(i,j)]     return p  def tabuleiro_preenche_posicao(t,c,v):     '''tabuleiro_preenche_posicao: tabuleiro x coordenada x inteiro -> tabuleiro     recebe um tabuleiro, uma coordenada(que verifica) e um inteiro(que verifica) e devolve um tabuleiro modificado na coordenada dada com o valor recebido'''     if e_coordenada(c) and isinstance(v,int):         t[coordenada_linha(c)-1][coordenada_coluna(c)-1]=v         return t         else:         raise ValueError('tabuleiro_preenche_posicao: argumentos invalidos')  def tabuleiro_actualiza_pontuacao(t,v):     '''tabuleiro_actualiza_pontuacao: tabuleiro x inteiro -> tabuleiro     recebe um tabuleiro(que verifica) e um inteiro multiplo de 4(que verifica) e devolve um tabuleiro com a pontuacao actualizada'''     if e_tabuleiro(t) and isinstance(v,int) and v>=0 and v%4==0:         t[-1]= t[-1]+ v      else:         raise ValueError('tabuleiro_actualiza_pontuacao: argumentos invalidos')      def tabuleiro_reduz(t,d):     '''tabuleiro_reduz: tabuleiro x cadeia de caracteres -> tabuleiro     recebe um tabuleiro e uma cadeia de caracteres com 4 posicoes e modifica e retorna o tabuleiro modificado de acordo com a cadeia de caracteres dada'''     if d in ['N', 'S', 'W', 'E']:         if d=='N':             for i in range(0,4):                 for j in range(0,3):                     if cria_coordenada(j+1,i+1) not in tabuleiro_posicoes_vazias(t):                         for c in range(j+1,4):                             if cria_coordenada(c+1,i+1) not in tabuleiro_posicoes_vazias(t):                                 if tabuleiro_posicao(t,cria_coordenada(j+1,i+1)) == tabuleiro_posicao(t,cria_coordenada(c+1,i+1)):                                     tabuleiro_preenche_posicao(t,cria_coordenada(j+1,i+1),tabuleiro_posicao(t,cria_coordenada(c+1,i+1))*2)                                     tabuleiro_preenche_posicao(t,cria_coordenada(c+1,i+1),0)                                     tabuleiro_actualiza_pontuacao(t,tabuleiro_posicao(t,cria_coordenada(j+1,i+1)))                                 break             for i in range(0,4):                 for j in range(0,3):                     if cria_coordenada(j+1,i+1) in tabuleiro_posicoes_vazias(t):                         for c in range(j+1,4):                             if cria_coordenada(c+1,i+1) not in tabuleiro_posicoes_vazias(t):                                 tabuleiro_preenche_posicao(t,cria_coordenada(j+1,i+1),tabuleiro_posicao(t,cria_coordenada(c+1,i+1)))                                 tabuleiro_preenche_posicao(t,cria_coordenada(c+1,i+1),0)                                 break                     elif d=='S':             for i in range(3,-1,-1):                 for j in range(3,0,-1):                     if cria_coordenada(j+1,i+1) not in tabuleiro_posicoes_vazias(t):                         for c in range(j-1,-1,-1):                             if cria_coordenada(c+1,i+1) not in tabuleiro_posicoes_vazias(t):                                 if tabuleiro_posicao(t,cria_coordenada(j+1,i+1)) == tabuleiro_posicao(t,cria_coordenada(c+1,i+1)):                                     tabuleiro_preenche_posicao(t,cria_coordenada(j+1,i+1),tabuleiro_posicao(t,cria_coordenada(c+1,i+1))*2)                                     tabuleiro_preenche_posicao(t,cria_coordenada(c+1,i+1),0)                                     tabuleiro_actualiza_pontuacao(t,tabuleiro_posicao(t,cria_coordenada(j+1,i+1)))                                 break             for i in range(3,-1,-1):                 for j in range(3,0,-1):                     if cria_coordenada(j+1,i+1) in tabuleiro_posicoes_vazias(t):                         for c in range(j-1,-1,-1):                             if cria_coordenada(c+1,i+1) not in tabuleiro_posicoes_vazias(t):                                 tabuleiro_preenche_posicao(t,cria_coordenada(j+1,i+1),tabuleiro_posicao(t,cria_coordenada(c+1,i+1)))                                 tabuleiro_preenche_posicao(t,cria_coordenada(c+1,i+1),0)                                 break                                     elif d=='W':             for i in range(0,4):                 for j in range(0,3):                     if cria_coordenada(i+1,j+1) not in tabuleiro_posicoes_vazias(t):                         for c in range(j+1,4):                             if cria_coordenada(i+1,c+1) not in tabuleiro_posicoes_vazias(t):                                 if tabuleiro_posicao(t,cria_coordenada(i+1,j+1)) == tabuleiro_posicao(t,cria_coordenada(i+1,c+1)):                                     tabuleiro_preenche_posicao(t,cria_coordenada(i+1,j+1),tabuleiro_posicao(t,cria_coordenada(i+1,c+1))*2)                                     tabuleiro_preenche_posicao(t,cria_coordenada(i+1,c+1),0)                                     tabuleiro_actualiza_pontuacao(t,tabuleiro_posicao(t,cria_coordenada(i+1,j+1)))                                 break             for i in range(0,4):                 for j in range(0,3):                     if cria_coordenada(i+1,j+1) in tabuleiro_posicoes_vazias(t):                         for c in range(j+1,4):                             if cria_coordenada(i+1,c+1) not in tabuleiro_posicoes_vazias(t):                                 tabuleiro_preenche_posicao(t,cria_coordenada(i+1,j+1),tabuleiro_posicao(t,cria_coordenada(i+1,c+1)))                                 tabuleiro_preenche_posicao(t,cria_coordenada(i+1,c+1),0)                                 break         elif d=='E':             for i in range(3,-1,-1):                 for j in range(3,0,-1):                     if cria_coordenada(i+1,j+1) not in tabuleiro_posicoes_vazias(t):                         for c in range(j-1,-1,-1):                             if cria_coordenada(i+1,c+1) not in tabuleiro_posicoes_vazias(t):                                 if tabuleiro_posicao(t,cria_coordenada(i+1,j+1)) == tabuleiro_posicao(t,cria_coordenada(i+1,c+1)):                                     tabuleiro_preenche_posicao(t,cria_coordenada(i+1,j+1),tabuleiro_posicao(t,cria_coordenada(i+1,c+1))*2)                                     tabuleiro_preenche_posicao(t,cria_coordenada(i+1,c+1),0)                                     tabuleiro_actualiza_pontuacao(t,tabuleiro_posicao(t,cria_coordenada(i+1,j+1)))                                 break             for i in range(3,-1,-1):                 for j in range(3,0,-1):                     if cria_coordenada(i+1,j+1) in tabuleiro_posicoes_vazias(t):                         for c in range(j-1,-1,-1):                             if cria_coordenada(i+1,c+1) not in tabuleiro_posicoes_vazias(t):                                 tabuleiro_preenche_posicao(t,cria_coordenada(i+1,j+1),tabuleiro_posicao(t,cria_coordenada(i+1,c+1)))                                 tabuleiro_preenche_posicao(t,cria_coordenada(i+1,c+1),0)                                 break                                     return t     else:         raise ValueError('tabuleiro_reduz: argumentos invalidos')      def e_tabuleiro(tab):     '''e_tabuleiro: universal -> logico     recebe um argumento e devolve True caso seja do tipo tabuleiro, False caso contrario'''     l = 0     if isinstance(tab, list) and len(tab)==5 and len(tab[0])==4 and len(tab[1])==4 and len(tab[2])==4 and len(tab[3])==4 and isinstance(tab[4],int) and tabuleiro_pontuacao(tab)>=0:         for i in range(len(tab)-1):             for j in range(len(tab)-1):                 if isinstance(tab[i][j],int):                     l = l+1         return l==16     else :         return False   def tabuleiro_terminado(t):     '''tabuleiro_terminado: tabuleiro -> logico     recebe um tabuleiro e devolve True se não for possivel mais nenhuma movimentacao atraves do tabuleiro_reduz em qualquer direcao e False caso ainda seja possivel movimentar em, pelo menos, uma direcao'''     t1 = copia_tabuleiro(t)     if tabuleiro_posicoes_vazias(t) == []:         if ((tabuleiro_reduz(t1,'N')) == t and (tabuleiro_reduz(t1,'S')) == t and (tabuleiro_reduz(t1,'E')) == t and (tabuleiro_reduz(t1,'W')) == t):             return True         else:             return False     return False    def copia_tabuleiro(t):     '''copia_tabuleiro: tabuleiro -> tabuleiro     recebe um tabuleiro e devolve outro tabuleiro igual ao recebido'''     tab_copia = cria_tabuleiro()     for i in range(4):         for j in range(4):             tab_copia[i][j] = t[i][j]     tab_copia[4] = t[4]     return tab_copia   def tabuleiros_iguais(t1,t2):     '''tabuleiros_iguais: tabuleiro -> logico     recebe dois tabuleiros e devolve True caso seja iguais, False caso contrario'''     return t1==t2   def escreve_tabuleiro(t):     '''escreve_tabuleiro: tabuleiro -> ()     recebe um tabuleiro(que verifica) e escreve no ecra esse mesmo tabuleiro'''     if e_tabuleiro(t):         for i in range(0,4):             for j in range(0,4):                 print('[', tabuleiro_posicao(t,cria_coordenada(i+1,j+1)),']',end=' ')             print()         print('Pontuacao:',tabuleiro_pontuacao(t))     else:         raise ValueError('escreve_tabuleiro: argumentos invalidos')   def pede_jogada():     '''pede_jogada: () -> cadeia de caracteres     nao recebe argumentos e pede ao utilizador uma cadeia de caracteres que indica a posicao para que este pretende fazer a sua jogada'''     while True:         direcao = input('Introduza uma direccao (N, S, E, W): ')         if direcao != 'N' and direcao != 'S' and direcao != 'W' and direcao != 'E':             print('Jogada invalida')         else:             return direcao              def preenche_posicao_aleatoria(tab):     '''preenche_posicao_aleatoria: tabuleiro -> tabuleiro x coordenadas_vazias e valor a adicionar     recebe um tabuleiro e devolve um tabuleiro modificado, uma lista com coordenadas aleatorias para ir mudar e escrever lá i'''     cord = tabuleiro_posicoes_vazias(tab)     if len(cord)!=0:         pos = int (random()*len(cord))         prob = random()         if prob >= 0.8:             i =4         if prob &lt;= 0.8:             i= 2         return tabuleiro_preenche_posicao(tab,cord[pos],i)       def jogo_2048():     '''jogo_2048:() -> ()     nao recebe nem retorna argumentos, serve para chamar as funcoes e para o utilizador jogar o jogo completo'''     t=cria_tabuleiro()     preenche_posicao_aleatoria(t)     while tabuleiro_terminado(t) == False:         preenche_posicao_aleatoria(t)         escreve_tabuleiro(t)         tabuleiro_reduz(t,pede_jogada())     print('GAME OVER!')
