# app-api-webhook-route.js
import { NextResponse } from 'next/server';

// 1. Handles Facebook/Instagram Webhook Verification (GET request)
export async function GET(request) {
  const url = new URL(request.url);
    const mode = url.searchParams.get('hub.mode');
      const token = url.searchParams.get('hub.verify_token');
        const challenge = url.searchParams.get('hub.challenge');

          // Replace 'mysecrettoken123' with whatever token you type into Meta Developers
            const MY_VERIFY_TOKEN = 'mysecrettoken123';

              if (mode && token) {
                  if (mode === 'subscribe' && token === MY_VERIFY_TOKEN) {
                        console.log('WEBHOOK_VERIFIED');
                              return new NextResponse(challenge, { status: 200 });
                                  } else {
                                        return new NextResponse('Forbidden', { status: 403 });
                                            }
                                              }
                                                return new NextResponse('Bad Request', { status: 400 });
                                                }

                                                // 2. Handles incoming messages/events (POST request)
                                                export async function POST(request) {
                                                  try {
                                                      const body = await request.json();
                                                          console.log('Received webhook event:', JSON.stringify(body, null, 2));

                                                              // Here is where you can handle incoming messages later

                                                                  return new NextResponse('EVENT_RECEIVED', { status: 200 });
                                                                    } catch (error) {
                                                                        console.error('Error handling webhook:', error);
                                                                            return new NextResponse('Internal Error', { status: 500 });
                                                                              }
                                                                              }
                                                                              