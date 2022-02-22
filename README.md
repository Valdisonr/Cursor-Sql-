# Cursor-Sql- deleta dados em tabelas distintas  não relacionadas.


procedure  ManutencaoImport
as
begin

select pessoas.id,pessoas.n_identificador, pessoas.nome,empresas.id,empresas.nome as empresa, (case 
                         when pessoas.estado = '0' then 'ATIVO' 
                         when PESSOAS.ESTADO='1' then 'BLOQUEADO'
                         end 
)as Estado
,classificacoes.id,classificacoes.descricao as Classificacao,estado from pessoas
inner join empresas on empresas.id=pessoas.empresa_id
inner join classificacoes on classificacoes.id=pessoas.classificacao_id where classificacoes.descricao='RESP.FINANCEIRO' and estado =1 
	EMPRESAS                     CLASSIFICACOES       
1	LA SALLE MANAUS               1-VISITANTE
3	FACULDADE LA SALLE            514 ALUNO-COLÉGIO
4	FAMILIAR ALUNO                516 ALUNO-FACULDADE
778	VISITANTE                 517 FUNCIONARIO(A)-COLEGIO
1968	PRESTADOR DE SERVICO      518 RESP. FINANCEIRO
5495	UNILASALLE EAD            521 RESP. EDUCACIONAL
                                529 PRESTADOR DE SERVIÇO 
                                531 FUNCIONARIO(A)-FACULDADE
                                532 ESPORTE COMUNIDADE
                                534 PRÉ-VESTIBULAR
                                535 RESP. MAE 
                                536 RESP. PAI
                                537 RELIGIOSO 
                                542 ALUNO-UNILASALLE-EAD
                                543-LANGUAGES COMUNIDADE


update pessoas set estado =1 where empresa_id=778  --BLOQUEIA-VISITANTE
update pessoas set estado =1 where empresa_id=1968 --BLOQUEIA- PRESTADOR DE SERVIÇO
update pessoas set estado =1 where empresa_id=4	--FAMILIAR ALUNO 
update pessoas set estado =1 where filtro2_id =1528
update pessoas set estado =1 where empresa_id=1 and classificacao_id=518
update pessoas set estado=1 where estado=0
SELECT *FROM PESSOAS WHERE estado = 0




end
