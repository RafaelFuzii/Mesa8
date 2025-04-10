o padrão de projeto Singleton  Essa implementação consiste em um Log Manager, isso é, um módulo que permite salvar logs do sistema Assim, seguindo o exemplo que foi passando em sala, realize as seguintes tarefas:
Crie uma classe chamada "LogManager" Essa é a classe na qual o padrão Singleton deve ser aplicado; 
A lista de logs deve ser persistida em memória, portanto, uma variável to tipo List pode ser útil
Escolher onde essa lista vai ser guardada faz parte do exercício;
Utilize alguma função do seu projeto para testar o LogManager
Por exemplo, registre uma mensagem de log para cada cliente cadastrado.
[PONTO EXTRA] Considerando a importância dos logs, seria interessante se TODAS as classes do sistemas pudessem fornecer seus próprios logs. Como desafio e valendo e valendo um 0.5pts extra, implemente uma solução para que cada classe possa forncer uma mensagem de log.
Dicas:
Um único LogManager deve ser dever ser capaz de gerenciar os logs todas as classes.
Evite a utilização de herança.

o codigo do service:
import { Injectable } from '@nestjs/common';
import { InjectModel } from '@nestjs/mongoose';
import { Model } from 'mongoose';
import { User, UserDocument } from './user.schema';
import { CreateUserDto } from './create-user.dto';

@Injectable()
export class UsersService {
  constructor(@InjectModel(User.name) private userModel: Model<UserDocument>) {}

  async create(createUserDto: CreateUserDto): Promise<User> {
    const createdUser = new this.userModel(createUserDto);
    return createdUser.save();
  }

  async findAll(): Promise<User[]> {
    return this.userModel.find().exec();
  }}
