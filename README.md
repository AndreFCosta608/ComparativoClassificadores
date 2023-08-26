# ComparativoClassificadores
* Fontes do artigo sobre a comparação de desempenho de topologias de redes neurais para a classificação de imagens.

					Um pequeno comparador de CNNs.

	Um problema recorrente em projetos envolvendo convolutional neural networks (CNNs) é a escolha da topologia de rede a ser utilizada. 
	Qual topologia trará maior precisão com o melhor desempenho para o projeto? 
	O primeiro passo para resolver este problema é estabelecer o tradeoff. Um limiar.... Ou mais especificamente... De quanta precisão o projeto realmente precisa. Será que 50% de precisão já atenderia com eficiência? Ou precisaria de mais? Algo como 70%, 80% ou 95%? Isto define a topologia. Pois quanto maior a precisão necessária, mais se exige da rede neural. 
	Logo, quanto mais a rede precisar entregar, maior ela terá de ser. Uma aplicação que examina exames médicos certamente irá precisar de um nível de precisão muito maior do que uma rede que apenas reconhece a silhueta humana em um contador de acesso. 

	Tendo definido o tradeoff o próximo passo é escolher a rede. 
	E nada melhor para ajudar nesta escolha do que testar algumas das principais topologias na prática. Assim sendo possível comparar os níveis de precisão de cada uma, os tempos necessários para resposta e quanto hardware foi necessário para alcançar os resultados..

	Para facilitar esta comparação apresentamos aqui um pequeno projeto contendo a implementação em python de algumas das principais topologias de redes configuradas para a funcão de classificação (aquelas que classificam o conteúdo da imagem, mas sem desenhar boundboxes ou a região de contorno). Assim como dois datasets com desafios diferentes. 
	Este projeto é mais voltado para facilitar quem trabalha com inteligência artificial embarcada. Aonde os recursos são normalmente escaços. Mas sendo útil também para projetos de baixo orçamento.

	Redes classificadoras podem trabalhar fazendo a classificação por texturas ou por objetos.  Por isto incluirmos 2 datasets. Um faz a classificação de tumores quanto a textura da imagem. Outro faz a classificação das folhas de oliveiras.
	IPC: Existem também topologias capazes de classificar quanto a forma e quanto a textura ao mesmo tempo. 
	Bom... Em tese, todas fazem exatamente isto... 
	Classificam como um todo. Forma e textura ao mesmo tempo. 
	Tanto que neste projeto utilizamos as exatas configurações para os dois desafios. 
	Mas é notório que determinadas topologias, com configurações de saídas específicas se saem melhor em um tipo de tarefa do que em outra.

	O projeto como um todo foi escrito de forma mais acadêmica. Evitando alguns métodos de frameworks que ocultam algumas etapas. Profissionalmente, para ganhar tempo, prefiro usar tais métodos. Como por exemplo a carga do dataset para a exposição à rede neural. Mas para efeitos didáticos fiz de uma forma um pouco menos automatizada, de forma a expor detalhes do funcionamento. Visando tornar mais acadêmico também evitei passar parâmetros por linha de comando. Deixando assim as configurações necessárias na forma de variáveis logo no início do código. Isto ganha tempo na hora de debugar e testar parâmetros diferentes.

	Procurei fazer a montagem de cada topologia com técnicas diferentes. Para tornar o projeto mais acadêmico. Algumas carregando diretamente a partir do framework, Outras incluindo camada a camada.

	Temos basicamente dois arquivos principais. Um para o treinamento das redes e outro para o teste de fogo... O "peso" para rodar uma rede vai depender de alguns fatores chave com: a topologia usada e o tamanho do seu dataset. Estes dois fatores combinados influenciam diretamente no tamanho final do arquivo de peso gerado. 
	Quanto maior ficar o arquivo peso, mais irá exigir do seu hardware. O que nos leva a mais um fator importante que é justamente o quanto de hardware se tem disponível. O treinamento sempre deverá ser feito em ambiente com GPUs. Mas o teste deverá ser feito em um hardware com capacidades o mais próximo possível do que será utilizado no ambiente de produção. Que poderá ser uma máquina core i3 ou mesmo uma Raspbery Pi. Assim os dados dos tempos de execução serão os mais próximos possíveis. Podendo ocorrer até mesmo do hardware não ser capaz de rodar determinada topologia a partir de um certo tamanho de dataset.

	É importante observar que cada topologia foi montada com uma certa quantidade de neurônios de entrada. Logo, o tamanho mínimo e máximo de imagem aceita já foi pré-definido. A rede U-net não funcionou para os dois datasets que foram inclusos no projeto. Mas como a uso em outros datasets ela foi mantida no script.

	Os resultados obtidos com os datasets demos com esta configuração mínima de camadas densas: 
	A tarefa de classificação de texturas se demostrou ser uma tarefa mais simples. 
	Aonde apenas as duas topologias mais leves não deram bons resultados (excluindo a U-net, pois precisaria ajustar a resolução). 
	Já a tarefa de classificação de imagens se demonstrou ser mais complicada do que parecia inicialmente. 
	Tendo somente as duas topologias maiores apresentado algum resultado que poderia ser aproveitado em um projeto com tradeoff mediano. 
	Já que parte do objetivo deste projeto é ser acadêmico, este dataset foi mantido. 
	
	Como possíveis causas para o baixo rendimento podemos citar: 
	
    1. Inicialmente a camada fraca de classificação utilizada (as camadas densas). Trabalhar em cima das camadas densas poderá melhorar o resultado. Como é um projeto de comparação apenas, não fiz tais testes.

    2. Fornecer mais informações para a rede aprender. No nosso caso, trabalhar com imagens um pouco maiores. Isto melhora a precisão, mas também aumenta consideravelmente o tamanho final do arquivo de peso do treinamento. Fazendo com que o processamento em produção se torne mais pesado. Podendo exigir o uso de uma GPU. 

    3. Devemos sempre por em cheque também a qualidade do dataset. Datasets para usos específicos, como o deste desafio 2, precisam de grande conhecimento técnico na área para ser montado ou mesmo validado. Lembre-se: Se alimentar a sua rede com lixo, ela irá produzir lixo. Como não possuo o conhecimento necessário para avaliar se a classificação manual e montagem do dataset foi bem feita, resta confiar no dataset que baixei gratuitamente. Mas se fosse um projeto profissional eu procuraria por profissionais capacitados na área para montar um dataset exclusivo para o projeto.


	Espero que este pequeno projeto seja útil. Tanto para contribuir com o aprendizado, quanto ajudar nas tarefas do dia a dia.

