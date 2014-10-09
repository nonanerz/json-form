# Json Form helper

Simply extend the `ApiController` and then use forms as you would normally, but they now expect to receive JSON.
Something like this.

[![Latest Stable Version](https://poser.pugx.org/mcfedr/json-form/v/stable.png)](https://packagist.org/packages/mcfedr/json-form)
[![License](https://poser.pugx.org/mcfedr/json-form/license.png)](https://packagist.org/packages/mcfedr/json-form)
[![Build Status](https://travis-ci.org/mcfedr/json-form.svg?branch=master)](https://travis-ci.org/mcfedr/json-form)

## Example

    class ActionController extends ApiController
        /**
         * @Route("/actions/{uuid}", requirements={"uuid"="[a-z0-9-]{36}"})
         * @Method("POST")
         */
        public function actionCreateAction(Request $request, $uuid) {
            $action = new Action();
            $form = $this->createForm(new ActionType(), $action);
            $this->handleJsonForm($form, $request);

            $em = $this->getDoctrine()->getManager();
            $em->persist($action);
            $em->flush();

            return new JsonResponse([
                'action' => $action
            ]);
        }
    }

## Tests

To run the tests

    ./vendor/bin/phpunit
