..  Copyright (C)  Brad Miller, David Ranum
    This work is licensed under the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by-nc-sa/4.0/.


.. Why Study Data Structures and Abstract Data Types?

Por que estudar Estruturas de Dados e Tipos de Dados Abstratos?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..  To manage the complexity of problems and the problem-solving process,
    computer scientists use abstractions to allow them to focus on the “big
    picture” without getting lost in the details. By creating models of the
    problem domain, we are able to utilize a better and more efficient
    problem-solving process. These models allow us to describe the data that
    our algorithms will manipulate in a much more consistent way with
    respect to the problem itself.

Para gerenciar a complexidade dos problemas e o processo de resolução de problemas,
os cientistas da computação usam abstrações para permitir que se concentrem no
corpo principal sem se perder nos detalhes. Criando modelos do
domínio do problema, somos capazes de utilizar um melhor e mais eficiente
processo de resolução de problemas. Esses modelos nos permitem descrever os dados que
nossos algoritmos manipularão de maneira muito mais consistente com
respeito ao problema em si.

..  Earlier, we referred to procedural abstraction as a process that hides
    the details of a particular function to allow the user or client to view
    it at a very high level. We now turn our attention to a similar idea,
    that of **data abstraction**. An **abstract data type**, sometimes
    abbreviated **ADT**, is a logical description of how we view the data
    and the operations that are allowed without regard to how they will be
    implemented. This means that we are concerned only with what the data is
    representing and not with how it will eventually be constructed. By
    providing this level of abstraction, we are creating an
    **encapsulation** around the data. The idea is that by encapsulating the
    details of the implementation, we are hiding them from the user’s view.
    This is called **information hiding**.

Anteriormente, nos referimos à abstração procedimental como um processo que oculta
os detalhes de uma função específica para permitir que o usuário ou cliente veja
de um nível muito alto. Agora voltamos nossa atenção para uma ideia semelhante,
o de **abstração de dados**. Um **tipo de dado abstrato**, às vezes
abreviado **ADT** (do inglês *Abstract Data Type*), é uma descrição lógica de como visualizamos os dados
e as operações que são permitidas sem considerar como elas são
implementadas. Isso significa que estamos preocupados apenas com o que os dados 
estão representando e não como será eventualmente construído. 
Fornecendo este nível de abstração, estamos criando um
**encapsulamento** em torno dos dados. A ideia é que encapsulando os
detalhes da implementação, estamos escondendo-os da visão do usuário.
Isso é chamado de **ocultação de informação**.


..  :ref:`Figure 2 <fig_adt>` shows a picture of what an abstract data type is and how it
    operates. The user interacts with the interface, using the operations
    that have been specified by the abstract data type. The abstract data
    type is the shell that the user interacts with. The implementation is
    hidden one level deeper. The user is not concerned with the details of
    the implementation.

A : ref: `Figura 2 <fig_adt>` mostra uma imagem de um tipo de dado abstrato e como ele
opera. O usuário interage com a interface, usando as operações
que foram especificadas pelo tipo de dado abstrato. O tipo de dado abstrato
é a capsula com a qual o usuário interage. A implementação é
escondida em um nível mais profundo. O usuário não está preocupado com os detalhes 
da implementação.

.. _fig_adt:

.. figure:: Figures/adt.png
   :align: center
   :scale: 50 %

   Figure 2: Tipo de Dado Abstrato

.. The implementation of an abstract data type, often referred to as a
    **data structure**, will require that we provide a physical view of the
    data using some collection of programming constructs and primitive data
    types. As we discussed earlier, the separation of these two perspectives
    will allow us to define the complex data models for our problems without
    giving any indication as to the details of how the model will actually
    be built. This provides an **implementation-independent** view of the
    data. Since there will usually be many different ways to implement an
    abstract data type, this implementation independence allows the
    programmer to switch the details of the implementation without changing
    the way the user of the data interacts with it. The user can remain
    focused on the problem-solving process.

A implementação de tipos de dados abstratos, geralmente chamado de
**estruturas de dados**, exigirá que forneçamos uma visão física dos
dados usando alguma coleção de construções de programação e tipos de dados 
primitivos. Como discutimos anteriormente, a separação dessas duas perspectivas
nos permitirá definir os modelos de dados complexos para os nossos problemas sem
dar qualquer indicação quanto aos detalhes de como o modelo realmente
será construído. Isso fornece uma visão **independente da implementação** dos
dados. Como normalmente haverá muitas maneiras diferentes de implementar um
tipo de dado abstrato, esta independência de implementação permite que o
programador mude os detalhes da implementação sem alterar
a maneira como o usuário dos dados interage com eles. O usuário pode permanecer
focado no processo de resolução de problemas.