<?php

namespace AppBundle\Controller;

use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Symfony\Component\HttpFoundation\Request;
use AppBundle\Entity\User;

class UserController extends Controller
{
    /*private  $user_data = [
        [
        "id" => 1,
        "name" => "Jayesh Jose",
        "email" => "josejayesh@gmail.com"
        ],
        [
        "id" => 2,
        "name" => "Anu Sebastian",
        "email" => "anuanncyannet@gmail.com"
        ],
        [
        "id" => 3,
        "name" => "Joseph Jayesh",
        "email" => "josephjayesh@gmail.com"
        ],
        [
        "id" => 4,
        "name" => "Aibel Jayesh",
        "email" => "aibeljayesh@gmail.com"
        ]
     ];*/
    /**
     * @Route("/", name="homepage")
     */
    public function indexAction(Request $request)
    {
        // replace this example code with whatever you need
        $data = [];
        //$data['clients'] = $this->user_data;
        $clients = $this->getDoctrine()
                         ->getRepository('AppBundle:User')
                         ->findAll();
        $data['clients'] = $clients;
        return $this->render('User/index.html.twig', $data);
    }
    
    /**
     * @Route("/registerUser", name="register")
     */
    public function registerAction(Request $request)
    {
        // replace this example code with whatever you need
        return $this->render('User/register.html.twig');
    }
    /**
     * @Route("/user/edit/{id}", name="edituser")
     */
    public function userEdit(Request $request, $id)
    {
        $data = [];
        $data["label"] = "Edit Employee Details";
        $client_repo = $this->getDoctrine()
                         ->getRepository('AppBundle:User');
        $form = $this ->createFormBuilder()
                      ->add('name')
                      ->add('email')
                      ->getForm()

        ;
        $form->handleRequest($request);
        $em = $this->getDoctrine()->getManager();
        if ($form->isSubmitted()) {
            $form_data = $form->getData();
            $client = $client_repo->find($id);
            $client->setName($form_data["name"]);
            $client->setEmail($form_data["email"]);
            $em->flush();
            return $this->redirectToRoute('homepage');
        } else {
            //$client_data = $this->user_data[$id-1];
            $client = $client_repo->find($id);
            $client_data['id'] = $client->getId();
            $client_data['name'] = $client->getName();
            $client_data['email'] = $client->getEmail();
            $data['form'] = $client_data;
        }
        return $this->render('User/form.html.twig', $data);
    }
    /**
     * @Route("/user/addNew", name="addNew")
     */
    public function userAdd(Request $request)
    {
        $data = [];
        $data["label"] = "Add New Employee";
        $form = $this ->createFormBuilder()
                      ->add('name')
                      ->add('email')
                      ->getForm()

        ;
        $form->handleRequest($request);
        if ($form->isSubmitted()) {
            $form_data = $form->getData();
            $data['form'] = [];
            $data['form'] = $form_data;
            $em = $this->getDoctrine()->getManager();
            $user = new User();
            $user->setName($form_data["name"]);
            $user->setEmail($form_data["email"]);
            $em->persist($user);
            $em->flush();
            return $this->redirectToRoute('homepage');
        }
        return $this->render('User/form.html.twig', $data);
    }
}
